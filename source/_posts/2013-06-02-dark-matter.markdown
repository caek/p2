---
layout: post
title: Uncovering Your Data's Dark Matter
subtitle: Want to see deeper patterns in your data? Try looking at it in a new way, says Jen Smith
permalink: /issue01/dark-matter/
byline: Jen Smith
category: issue01
authors:
    - name: Jen Smith
      twitter: jennifersmithco
      avatar: jen-avatar.jpg
---
> "Lateral thinking is... concerned with breaking out of the concept prisons of old ideas. This leads to changes in attitude and approach; to looking in a different way at things which have always been looked at in the same way." - Edward De Bono

We write applications which report on data in systems every day. And that data is a rich source of information that is used to understand your business and your customers better. What isn’t obvious is that this data can tell you more about your customers if you can see it in a different way.

But getting a fresh perspective on your existing data in its existing structure can be harder than it looks.  Your lines of investigation are constrained by the medium in which you store the data. We have to put into a fresh context to really see the patterns which tell a story. By exploring your data freed up from it's normal environments, you may discover insights and ideas. Lets have a look at some of the challenges here.

I was working with a client recently who wanted use their data to examine how their users interacted with the site and with each other. Their database contained several years worth of transactional data: they knew the answer would be in there. But their existing database made it hard to find the information they wanted. Trying to query interactions and relationships between users in the existing, relational database  quickly descended into complicated join statements and temporary tables. Aside from performance problems, the complexity of the SQL statements made the whole venture extremely frustrating.

This is a common problem. When choosing a database technology and structure we – quite reasonably – make our decision based on the best fit for the application. Unfortunately the choices we make can later constrain our ability to analyse and explore the data. So we decided that we had to break the data out of its existing structure and model it in a new way.

As a proof-of-concept, we loaded two years of data into a graph database. We didn't spend long developing a mature Extract-Transform-Load (ETL) process. It was more important to us to get feedback quickly on whether our approach was working.

Graph databases store data as graphs of nodes and relationships. For example, if you were analysing data from an online record store, you might model an album purchase as follows:

![A simple relationship](/p2/images/dark-matter/1.png)

As it stands, this resembles the original, relational database structure. Users, albums and artists, originally stored as tables, are now represented as nodes. Likewise, purchase information and links between albums and artists are now named, directed relationships between these nodes.

Things start to get interesting when you start to infer new relationships from the existing data and overlay them on the graph. For example, you could infer that I like Aphex Twin if I have bought two of his albums:

![Inferred Relationship](/p2/images/dark-matter/2.png)

Now from a simple database of music purchases, you can build up a graph of users and their preferred artists. You can start to use this information to start recommending music to me that I might enjoy:

![Recommending Music](/p2/images/dark-matter/3.png)

Perhaps I would enjoy Squarepusher too as my friend Bob - a fellow Aphex Twin enthusiast - is a fan.

Graph database show their strength when you introduce graph theory. The shortest path between Aphex Twin and Squarepusher can indicate their musical similarity. You can cluster artists by their fan’s tastes or calculate the clustering coefficient to measure whether users purchase a broad range of genres or they are all really into Drill n' Bass.

The graph database allowed us to traverse relationships in our data that were hard to access in the original structure. This solved our initial problem, but more excitingly than that, simply changing the way we stored our data opened up a wealth of new ideas and possibilities that we had not thought of before.

Graphs are a powerful way of modelling your data to discover new insights, but other database technologies can open up different areas of exploration. For example, Datomic organises data as a series of time based facts allowing you to explore user behaviour over time such as “2013-02-04 Jen bought ‘Classics’. Document databases are great for unstructured data and relational databases are still great for aggregating and slicing up data. When was the last time you de-normalised a NoSQL store into DB2 to glean insight?

> "A moment's insight is sometimes worth a life's experience." - Oliver Wendell Holmes, Jr.
