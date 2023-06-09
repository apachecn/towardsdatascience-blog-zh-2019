# 为数据科学创建一个简单的网站抓取器

> 原文：<https://towardsdatascience.com/creating-an-easy-website-scraper-for-data-science-sports-prediction-pt-1-f024abd53861?source=collection_archive---------23----------------------->

![](img/0f72f4a9e3ac3d50a333af037749fbb4.png)

收集数据是任何机器学习项目的重要部分，但许多教程倾向于使用已经以方便的格式存在的数据。这对于案例来说是很好的，但是对于学习整个过程来说不是很好。在现实世界中，并不是所有的数据都可以在谷歌上找到…至少现在还不行。这是教程的一部分，我们收集所有必要的统计数据来训练我们的神经网络进行 NHL 预测，但更重要的是，我将向您展示如何应用这些概念并从万维网上收集您想要的任何数据。

## 突出

*   构建刮擦环境
*   使用 selenium 删除 HTML
*   用*美颜组*处理
*   写入 CSV 文件

## 先决条件

*   必须能够理解 Python

# 1-概述

对于这个例子，我们将采用整个赛季的 NHL 每日游戏统计数据。输出将由两行数据组成，每行是一个队对比赛的看法。这些数据将以 **CSV** (逗号分隔值)格式保存到一个文本文件中，这本质上只是一个 excel 工作表，但它没有用线来分隔单元格，而是用逗号和换行符。作为参考，我们将从 NHL.com 每日统计页面的[开始，以包含 2.1k 行的输出文件结束:](http://www.nhl.com/stats/team?reportType=game&dateFrom=2018-10-10&dateTo=2018-10-10&gameType=2&filter=gamesPlayed,gte,1&sort=points,wins)

![](img/7789c94a3937878e197ddf7695b51f7e.png)

A single day worth of data, in CSV format

## 这项工作所需的工具

```
from bs4 import BeautifulSoup as soup
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from numpy import array
import pandas as pdimport csv
from datetime import date
```

Selenium 本质上是一个库，它可以打开一个 web 浏览器实例并自动与之交互，而 BeautifuSoup 是从页面中提取 HTML 以供我们使用的。 *Numpy* 和 *Pandas* 都用于数据处理和格式化，如果你只是想制作一个 web scraper，这是不需要的，但是因为我们稍后将在 *Tensorflow* 中使用这些数据，所以立即使用 Numpy 数组是最容易的，特别是考虑到我对这些数据的计划(更不用说它比常规 Python 逻辑更有效)。

# 2-网页到 HTML

进入实际的抓取，我们首先需要一个可以访问网页的功能，并把它变成更加用户友好的东西。实现这一点的计划是简单地创建一个简短的方法，该方法将在 selenium 中打开页面，获取 HTML(每个网页都有的基于文本的框架)，将其转换成可以使用的**汤**，然后将其返回给用户。

这个简短的方法完成了实际“刮擦”的所有步骤。如果你给它一个 URL，页面的 HTML 将会以一种功能性的格式返回，你可以从中找到你所需要的内容。让我们深入了解它的工作原理。

```
def url_to_soup(url):
    # selenium driver setup
    driver = webdriver.Firefox() # get url
    driver.get(url) # create sauce (raw HTML) using driver
    source = driver.page_source
    driver.close() 
```

第一步是定义一个 **web 驱动程序**，它本质上就是 selenium 将要使用的浏览器。我喜欢 Selenium 的一点是，它可以实时自动打开网页，这样你就可以看到程序的每个动作。我决定用火狐。你可以使用任何浏览器，selenium 将完成访问该浏览器的所有工作，这非常简单，只需定义你想使用的浏览器。现在你所要做的就是给驱动一个 URL，它会自动打开页面，但是不要忘记一旦你完成了从页面中拉出，就关闭**驱动**。

**源**变量包含从页面中提取的原始 HTML。我用“原始”这个词是因为它就是这样，原始而杂乱。我们必须首先把这种文本风暴变成我们可以轻松享用的汤。因此，我们简单地通过接受两个输入的“soup”函数来运行它；源页面和**解析器**。

解析器函数不是您可能知道的解析器。您可以查看 [B.S .文档](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)来找到不同种类的解析器，但是它们都做相同的事情，即清理 HTML 以便我们可以用自己的代码解析它。有些可能行得通，有些则不行，但在这种情况下,‘lxml’恰好做到了。不过有一个技巧。在指定解析器之前，必须打开命令行并下载解析器。既然我选择了 lxml，我必须首先做:

```
$ pip install lxml
```

在这之后，您就可以运行接下来的两行代码了…

```
# soup(input, parser)
url_soup = soup(sauce, 'lxml')# return the parsed soup
return url_soup
```

# 3-收集有效数据

在我们能消化汤之前，我们需要先收集它。到目前为止，我们所做的只是定义了一个从单个网页中删除数据的方法，但是我们需要整个赛季的每日游戏数据，所以我们将多次调用这个方法。因此，首先我们需要找出一种方法来快速收集所有这些信息，并将其保存在一起进行处理。

理解这个 web scraper 的一个重要概念是 URL 的操作。NHL 网站碰巧对表中的每个统计数据实例都使用相同的 URL 结构。下面是一个 NHL.com 每日统计页面的链接。如你所见，这个 URL 中嵌入了一个日期，在两个不同的地方。**如果您将这些更改为不同的日期，您会发现该链接仍然有效，您将被重定向到包含该特定日期统计数据的页面。**

```
[http://www.nhl.com/stats/team?reportType=game&dateFrom=2018-10-08&dateTo=2018-10-08&gameType=2&filter=gamesPlayed,gte,1&sort=points,wins](http://www.nhl.com/stats/team?reportType=game&dateFrom=2018-10-08&dateTo=2018-10-08&gameType=2&filter=gamesPlayed,gte,1&sort=points,wins)
```

我们可以利用这一点，只需自动修改嵌入 URL 的日期。为了让我们将这个概念付诸实施，我们需要一个函数，它将为任何特定日期生成到 NHL.com 页面的链接，这正是下面五行代码所做的。

```
def nhl_daily_data(year, month, day):
    nhl_daily = f"[http://www.nhl.com/stats/team?reportType=game&dateFrom={year}-{month}-{day}&dateTo={year}-{month}-{day}&gameType=2&filter=gamesPlayed,gte,1&sort=points,wins](http://www.nhl.com/stats/team?reportType=game&dateFrom={year}-{month}-{day}&dateTo={year}-{month}-{day}&gameType=2&filter=gamesPlayed,gte,1&sort=points,wins)"
    nhl_soup = url_to_soup(nhl_daily)
```

该函数通过使用 f 字符串来实现这一点。您可能不熟悉这个工具，但它是 Python 3.6 的默认版本。实际上，无论您在函数的参数中输入什么日期，f 字符串都会填充 NHL.com URL 中的年、月和日位置。然后，它利用前面的 **url_to_soup()** 函数来返回该页面的 soup。所以不用分别调用这两个函数，这个函数会替你做。

例如，如果您想要查找 2018 年 10 月 8 日玩的游戏的统计数据，您可以使用这些参数调用函数: **nhl_daily_data(2018，10，08)** ，然后它会从[这个特定的 NHL.com 网页中提取调味汁，](http://www.nhl.com/stats/team?reportType=game&dateFrom=2018-10-08&dateTo=2018-10-08&gameType=2&filter=gamesPlayed,gte,1&sort=points,wins)通过解析器运行它，并以汤的形式返回它。

您可能会问自己，为什么在您的项目中需要这个函数？事实是，也许你不知道。找到网络数据的第一步是想出一个攻击计划。也许你想要的所有信息都存储在同一个页面上，在这种情况下，你可以跳过这一步，只需一次扫描就可以得到你需要的所有数据。如果你不能使用这个 URL 技巧，selenium 提供了“手动”点击的功能，你可以使用它来浏览网站，你可以在 Selenium 的[文档中找到这些功能。](https://selenium-python.readthedocs.io/navigating.html)

接下来，我将亲自讲解如何阅读 HTML，这样你就可以告诉你的程序要寻找什么。

## 3.1-阅读 HTML

为了完成下一部分，你需要知道如何阅读 HTML。第一步是导航到你需要数据的页面，我去了一个随机的[每日 NHL 统计页面](http://www.nhl.com/stats/team?reportType=game&dateFrom=2018-10-08&dateTo=2018-10-08&gameType=2&filter=gamesPlayed,gte,1&sort=points,wins)。看看你的数据在页面上的位置。你可以看到游戏的统计数据都被嵌入到某种表格中，所以很可能这个表格是它自己的类。您的数据可能不像我的数据一样在一个独特的 JavaScript 元素中，但是过程仍然是一样的。

接下来，右键单击要使用的文本信息，然后按“检查元素”。这将在您的 web 浏览器中打开检查窗格，您可以在其中找到该页面的所有类和子类。浏览这些，找到你想要的对象、图表或信息所在的类的“路线”。你需要这个来告诉你的铲运机去哪里找。

![](img/8b95b15d5510cececc0addad3b9bb84e.png)

When selecting the “rt-table” class, the table on the web page is highlighted.

**find()** 函数是在代码中寻找你所需要的东西。我们不需要让程序遍历 HTML 中的每个文件夹来找到表格，你只需要指定要查找哪个类，然后 *BeautifulSoup* 就会找到它。

```
# finding table data
table_body = nhl_soup.find(attrs="rt-table").find(attrs='rt-tbody')
```

这个一行程序在 python 中定位保存表数据的类，并将其转换为对象“table _ body**”**，然后我们可以解析该对象来记录我们需要的数据。

该表实际上是二维数组的格式；每个游戏有两个数组。每个数组都是一个队对那场比赛的看法的统计数据。

## 3.2-收集信息

下面的大块代码可能看起来很难，但实际上我们已经到了最后阶段。

```
# loading the game data
game_data = []# finding the chart and looping through rows
for rows in table_body.find_all(attrs="rt-tr-group"):
    row_data = []
```

通过阅读 HTML，我们可以简单地使用 **find()** 函数，并在它前面放置一个 for 循环，它将自动提取类中的所有内容，一次一行。但是我们不能就此止步，因为 table 元素中包含的不仅仅是我们想要的数据，还有一些我们不想要的数据，比如标题和分部。如果我们查看表的数据部分的特定 HTML，可以看到它有一个不同的标签: **td** (表数据)。这意味着我们需要做一个嵌套的 for 循环，以便将搜索范围缩小到这个表数据。

```
 # looping through row data
    for td in rows.find_all():
         row_data.append(td.text)
         game_date = f"{year}-{month}-{day}" enemy_team = row_data[4][14:].lstrip()
         win = row_data[8]
         loss = row_data[9]
         over_time = row_data[11]
         points = row_data[12]
         goals_for = row_data[13]
         goals_against = row_data[14]
         shots_for = row_data[17]
         shots_against = row_data[18]
         power_play_goals_for = row_data[19]
         power_play_opportunities = row_data[20]
         power_play_percent = row_data[21]
         power_play_goals_against = row_data[23]
         penalty_kill_percent = row_data[24]
         faceoff_wins = row_data[25]
         faceoff_losses = row_data[26]
         faceoff_win_pct = row_data[27]row_data = [game_date, team_name, enemy_team, home_away, win,   loss, over_time, points, goals_for, goals_against, shots_for, shots_against, power_play_goals_for, power_play_opportunities, power_play_percent, power_play_goals_against, penalty_kill_percent, faceoff_wins, faceoff_losses, faceoff_win_pct]
    game_data.append(row_data)
    return game_data
```

这为我们找到了行数据的列表，一次一行。然后，我们可以选择我们想要的信息，对其进行分类并保存。

## 4-唯一剩下要做的事…省省吧

为了把它包装成一个我们可以使用的漂亮的蝴蝶结，我定义了一个批处理收集方法。这个方法调用 **nhl_daily_data()** 方法，在一个日期范围内一次调用一天。这将为我们收集的所有内容创建一个图表，然后将其作为 CSV 文件写入您的计算机。

```
def batch_collection(start_date, end_date):
    season_dates = pd.date_range(start=start_date, end=end_date)
    for date in season_dates:
        print(date)
        year = date.year
        month = date.month
        day = date.day
        chart = array(nhl_daily_data(year, month, day)) # .txt to CSV
        with open('2017-2018season.txt', "a") as output:
            writer = csv.writer(output, lineterminator='\n')
            writer.writerows(chart)
```

从这里开始，这些数据将需要更多的处理，但我们需要的一切现在都以一种易于阅读的格式集中到一个文件中。