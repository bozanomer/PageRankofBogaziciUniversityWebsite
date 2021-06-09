Simple Python Search Spider, Page Ranker, and Visualizer

This is a set of programs that emulate some of the functions of a
search engine.  They store their data in a SQLITE3 database named
'spider.sqlite'.  This file can be removed at any time to restart the
process.

You should install the SQLite browser to view and modify
the databases from:

http://sqlitebrowser.org/

This program crawls a web site and pulls a series of pages into the
database, recording the links between pages.

Note: Windows has difficulty in displaying UTF-8 characters
in the console so for each console window you open, you may need
to type the following command before running this code:

    chcp 65001

http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how

Mac: rm spider.sqlite
Mac: python3 spider.py

Win: del spider.sqlite
Win: spider.py

Enter web url or enter: http://www.boun.edu.tr/
['http://www.boun.edu.tr/']
How many pages:2
238 http://www.boun.edu.tr/Default.aspx?SectionID=1067 (26478) 70
247 http://www.boun.edu.tr/Default.aspx?SectionID=867 (26429) 70
How many pages:

In this sample run, we told it to crawl a website and retrieve two
pages.  If you restart the program again and tell it to crawl more
pages, it will not re-crawl any pages already in the database.  Upon
restart it goes to a random non-crawled page and starts there.  So
each successive run of spider.py is additive.

Mac: python3 spider.py
Win: spider.py

Enter web url or enter: http://www.boun.edu.tr/
['http://www.boun.edu.tr/']
How many pages:3
185 http://www.boun.edu.tr/Default.aspx?SectionID=1080 (25351) 63
254 http://www.boun.edu.tr/Default.aspx?SectionID=869 (27083) 70
133 http://www.boun.edu.tr/Default.aspx?SectionID=162 (49822) 75
How many pages:

You can have multiple starting points in the same database -
within the program these are called "webs".   The spider
chooses randomly amongst all non-visited links across all
the webs.


If you want to dump the contents of the spider.sqlite file, you can
run spdump.py as follows:

Mac: python3 spdump.py
Win: spdump.py

(50, 1.0, 3.5032374661864534, 73, 'http://www.boun.edu.tr/tr_TR/Content/Kampus_Yasami/KampusUlasimPark')
(50, 1.0, 3.5032374661864534, 66, 'http://www.boun.edu.tr/Default.aspx?SectionID=939')
(50, 1.0, 3.5210739275250718, 62, 'http://www.boun.edu.tr/Default.aspx?SectionID=959')
(50, 1.0, 3.5032374661864534, 55, 'http://www.boun.edu.tr/Default.aspx?SectionID=927')
(50, 1.0, 3.5366799032776126, 51, 'http://www.boun.edu.tr/Default.aspx?SectionID=43')
....


This shows the number of incoming links, the old page rank, the new page
rank, the id of the page, and the url of the page.  The spdump.py program
only shows pages that have at least one incoming link to them.

Once you have a few pages in the database, you can run Page Rank on the
pages using the sprank.py program.  You simply tell it how many Page
Rank iterations to run.

Mac: python3 sprank.py
Win: sprank.py

How many iterations:5
1 0.9303032529242404
2 0.09752225005441273
3 0.03129981477719415
4 0.01609582336277218
5 0.013486999226824968
[(1, 0.7075460919808206), (2, 1.5479459564157538), (3, 0.38723324931435976), (4, 0.7366017558811464), (9, 0.3400122988805731)]

You can dump the database again to see that page rank has been updated:

Mac: python3 spdump.py
Win: spdump.py

(50, 1.0, 3.5032374661864534, 73, 'http://www.boun.edu.tr/tr_TR/Content/Kampus_Yasami/KampusUlasimPark')
(50, 1.0, 3.5032374661864534, 66, 'http://www.boun.edu.tr/Default.aspx?SectionID=939')
(50, 1.0, 3.5210739275250718, 62, 'http://www.boun.edu.tr/Default.aspx?SectionID=959')
(50, 1.0, 3.5032374661864534, 55, 'http://www.boun.edu.tr/Default.aspx?SectionID=927')
(50, 1.0, 3.5366799032776126, 51, 'http://www.boun.edu.tr/Default.aspx?SectionID=43')
....

You can run sprank.py as many times as you like and it will simply refine
the page rank the more times you run it.  You can even run sprank.py a few times
and then go spider a few more pages sith spider.py and then run sprank.py
to converge the page ranks.

If you want to restart the Page Rank calculations without re-spidering the
web pages, you can use spreset.py

Mac: python3 spreset.py
Win: spreset.py

All pages set to a rank of 1.0

Mac: python3 sprank.py
Win: sprank.py

How many iterations:50
1 1.0525855625912244
2 0.1330520192849148
3 0.04509250607390078
4 0.019609524109159164
5 0.012336420418619595
6 0.010608638481425608
7 0.009756972570032194
8 0.008971341352905894
9 0.008331179849559096
10 0.007726851871071246
11 0.0071724620005048055
12 0.006658411430876473
13 0.006181100261157297
14 0.00573844078632344
15 0.005327321383926418
16 0.004945766783295648
17 0.0045914998940510795
18 0.004262629677217201
19 0.003957308224259201
20 0.003673859136628542
21 0.0034107117132097576
22 0.003166413062552721
23 0.002939612696584402
24 0.002729057354319538
25 0.0025335834421155302
26 0.002352110716361562
27 0.002183636321994549
28 0.0020272292245584684
29 0.001882025083108014
30 0.0017472214636462308
31 0.0016220734094637428
32 0.001505889322192768
33 0.0013980271407519325
34 0.001297890792812866
35 0.0012049269008942898
36 0.0011186217242145824
37 0.0010384983196526083
38 0.0009641139060473418
39 0.0008950574172761673
40 0.000830947230609599
41 0.000771429057766434
42 0.0007161739870424468
43 0.000664876665653259
44 0.0006172536122897815
45 0.0005730416505312691
46 0.0005319964544636227
47 0.0004938911984830334
48 0.0004585153038005474
49 0.000425673274731446
50 0.00039518361834193263
[(1, 0.022904162341069803), (2, 0.05017209929915698), (3, 0.012553746913903622), (4, 0.023897157897976775), (9, 0.011026708583923331)]

For each iteration of the page rank algorithm it prints the average
change per page of the page rank.   The network initially is quite
unbalanced and so the individual page ranks are changing wildly.
But in a few short iterations, the page rank converges.  You
should run prank.py long enough that the page ranks converge.

If you want to visualize the current top pages in terms of page rank,
run spjson.py to write the pages out in JSON format to be viewed in a
web browser.

Mac: python3 spjson.py
Win: spjson.py

Creating JSON output on spider.js...
How many nodes? 30
Open force.html in a browser to view the visualization


You can view this data by opening the file force.html in your web browser.
This shows an automatic layout of the nodes and links.  You can click and
drag any node and you can also double click on a node to find the URL
that is represented by the node.

This visualization is provided using the force layout from:

http://mbostock.github.com/d3/

If you rerun the other utilities and then re-run spjson.py - you merely
have to press refresh in the browser to get the new data from spider.js.
