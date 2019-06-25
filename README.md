# Big-Cases
This is the basic Python code behind the [@big_cases Twitter bot](http://twitter.com/big_cases).

The bot uses PACER RSS feeds to gather the latest filings from 74 U.S. District Courts and five federal courts of appeals and stores the docket entries in a database. It matches new filings against a preselected list of major cases, scrapes matching documents from PACER, uploads them to both a [DocumentCloud](http://www.documentcloud.org) project and the RECAP archive, then posts the results on Twitter. 

Note that some federal district courts -- including those in the Eastern District of Virginia, the District of Maryland and the District of Hawaii --  have elected not to publish an RSS feed from their dockets. As a result, Big Cases can't follow cases in those districts. Most federal courts of appeal also do not publish RSS feeds of new docket entries.

(A separate part of the bot gathers docket information from the U.S. Supreme Court's electronic filing system.)

## How it basically works

Big-Cases uses three main Python scripts to gather docket entries, scrape dockets and tweet the results. This is mostly a vestigate of the fact that the bot was built as an add-on to a larger scraping tool. The scripts run in order, every four minutes:

* **pacer_rss.py** - Scrapes PACER's RSS feeds, matches them against a list of selected cases and stores the results in a MySQL database.
* **bigcases_scrape_docs.py** - Attempts to scrape documents from PACER based on new matches identified from RSS feeds. It also publishes the results on DocumentCloud and the RECAP archive.
* **bigcases.py** - Tweets the results.

## Settings and lists of stuff

The list of cases Big-Cases is following is stored in **bigcases_list.py**; the list of available PACER RSS feeds is stored in **pacer_rss_feeds.py**. 

## Yes, the robot listens

A separate secript, **bigcases_listen.py** periodically checks the bot's Twitter mentions for new cases to follow, parses the requests and matches them against courts with active data feeds and cases that already exist in the database.

## Other stuff to know

Big-Cases has only been tested on a machine running CentOS Linux 7. 

## Dependencies

  pip install python-documentcloud

Customize `bigcases_settings` with credential information for PACER,
DocumentCloud, Twitter, RECAP, &c.
