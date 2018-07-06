# Coursera Big Data Analysis
Repository for the Big Data Analysis: Hive, Spark SQL, DataFrames and GraphFrames course.

## Task 1 - Hive Assignment 1. DDL: Create Tables
The purpose of this task is to create an external table on the posts data of the 
stackoverflow.com website.

* Create your own database and 'use' it. 
* Create external table 'posts_sample_external' over the sample dataset with posts in 
'/data/stackexchange1000' directory. 
* Create managed table 'posts_sample' and populate with 
the data from the external table. 
  - 'Posts_sample' table should be partitioned by year and 
by month of post creation.
* Provide output of query which selects lines number per each partition in the format:
"year  month count " where year in YYYY format and month in YYYY-MM format. 
  - The result is the 3th line of the last query output.

### Dataset's description
The input dataset contains two parts: users and posts (questions and answers) from StackOverflow site.
Posts are in XML format, but it doesn't matter: you can interpret it as a text of independent lines, one post per each line.  

```
<row Id="11" PostTypeId="1" AcceptedAnswerId="1248" CreationDate="2008-07-31T23:55:37.967"
 Score="1106" ViewCount="115048" Body="&lt;p&gt;Given a specific &lt;code&gt;DateTime&lt;
 /code&gt; value, how do I display relative time, like:&lt;/p&gt;&#xA;&#xA;&lt;ul&gt;&#xA;
 &lt;li&gt;2 hours ago&lt;/li&gt;&#xA;&lt;li&gt;3 days ago&lt;/li&gt;&#xA;&lt;li&gt;
 a month ago&lt;/li&gt;&#xA;&lt;/ul&gt;&#xA;" OwnerUserId="1" LastEditorUserId="1136709"
 LastEditorDisplayName="user2370523" LastEditDate="2015-12-29T02:08:37.450" 
 LastActivityDate="2016-07-13T23:23:58.537" Title="How can relative time be calculated in C#?"
 Tags="&lt;c#&gt;&lt;datetime&gt;&lt;datediff&gt;&lt;relative-time-span&gt;"  AnswerCount="33" 
 CommentCount="4" FavoriteCount="508" CommunityOwnedDate="2009-09-04T13:15:59.820" />
```

So, the lines not started with the "row" tags should be ignored. The valid row contains the following fields and their order is not defined:

*  Id (integer) - id of the post
*  PostTypeId (integer: 1 or 2) - 1 for questions, 2 for answers
*  CreationDate (date) - post creation date in the format "YYYY-MM-DDTHH:MM:SS.ms"
*  Tags (string, optional) - list of post tags, each tag is wrapped with html entities '&lt;' and '&gt;'
*  OwnerUserId (integer, optional) - user id of the post's author
*  ParentId (integer, optional) - for answers - id of the question
*  Score (integer) - score (votes) of a question or an answer, can be negative (!)
*  FavoriteCount (integer, optional) - how many times the question was added in the favorites
