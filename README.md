# Coursera Big Data Analysis
Repository for the Big Data Analysis: Hive, Spark SQL, DataFrames and GraphFrames course.


## Dataset's description
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

So, the lines not started with the "row" tags should be ignored. 
The valid row contains the following fields and their order is not defined:

*  Id (integer) - id of the post
*  PostTypeId (integer: 1 or 2) - 1 for questions, 2 for answers
*  CreationDate (date) - post creation date in the format "YYYY-MM-DDTHH:MM:SS.ms"
*  Tags (string, optional) - list of post tags, each tag is wrapped with html entities '&lt;' and '&gt;'
*  OwnerUserId (integer, optional) - user id of the post's author
*  ParentId (integer, optional) - for answers - id of the question
*  Score (integer) - score (votes) of a question or an answer, can be negative (!)
*  FavoriteCount (integer, optional) - how many times the question was added in the favorites

The second part of the dataset contains StackOverflow users. 
The format is similar to the posts, example:
```
<row Id="4" Reputation="26638" CreationDate="2008-07-31T14:22:31.317" DisplayName="Joel Spolsky" 
LastAccessDate="2016-12-10T22:12:46.367" WebsiteUrl="http://www.joelonsoftware.com/" 
Location="New York, NY" AboutMe="&lt;p&gt;I am:&lt;/p&gt;&#xA;&#xA;&lt;ul&gt;&#xA;&lt;
li&gt;the co-founder and CEO of &lt;a href=&quot;http://stackexchange.com">Stack Exchange&lt;
/a&gt;&lt;/li&gt;&#xA;&lt;li&gt;the co-founder of &lt;a href=&quot;http://www.fogcreek.com" 
rel=&quot;nofollow&quot;&gt;Fog Creek Software&lt;/a&gt;&lt;/li&gt;&#xA;&lt;li&gt;
the creator and chairman of the board of &lt;a href=&quot;http://trello.com" 
rel=&quot;nofollow&quot;&gt;Trello&lt;/a&gt;&lt;/li&gt;&#xA;&lt;li&gt;owner of Taco,
 the most famous Siberian Husky on the Upper West Side.&lt;/li&gt;&#xA;&lt;/ul&gt;
 &#xA;&#xA;&lt;p&gt;You can find me on Twitter (as &lt;a href=&quot;http://twitter.com/spolsky" 
 rel=&quot;nofollow&quot;&gt;@spolsky&lt;/a&gt;) or on my rarely-updated blog, 
 &lt;a href=&quot;http://joelonsoftware.com" rel=&quot;nofollow&quot;&gt;
 Joel on Software&lt;/a&gt;.&lt;/p&gt;&#xA;" Views="66761" UpVotes="779" DownVotes="96" 
 ProfileImageUrl="https://i.stack.imgur.com/C5gBG.jpg?s=128&g=1" AccountId="4" />
```
The fields are the following and their order is also not defined:

*  Id (integer) - user id
*  Reputation (integer) - user's reputation
*  CreationDate (string) - creation date in the format "YYYY-MM-DDTHH:MM:SS.ms"
*  DisplayName (string) - user's name
*  Location (string, options) - user's country
*  Age (integer, optional) - user's age


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

## Task 2 - Hive Assignment 2. DML: Find Most Popular Tags
Compare most popular tags in year 2016 with tags in 2009. Tag popularity is the number of questions (post_type_id=1) with this tag.  
 Output top 10 tags in format:
 ```
 tag, rank in 2016, rank in 2009, tag popularity in 2016, tag popularity in 2009
 ```
 