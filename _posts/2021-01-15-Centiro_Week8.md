---
layout: post
title: "Centiro Internship Week Eight"
categories: [The Internship]
---

## We are writing code!!!

Last week's hard work on reading documentation and looking at legacy code finally payed of.
A new version of a Api was created in a TFS repository. CodeReviews where planned at every CheckIn because it was a environment reaching production at the end.

Stepping through the process starting with all queries that should be made to the database.
Using SSMS to test them all and then moving them into our RequestHandler in code.

For more complex queries we began using SqlBuilder. Soon we realized that SqlBuilder wasn't sophisticated enough and moved over to using simple strings instead. This made it more clear on what the query was doing.
If someone else would look at the code he/she could simply copy the query string and paste it inside a .sql file and run it against the database to explore the result. Formatting the query string was also easy in code because it worked even with a lot of spaces and line-breaks. I wanted a consistent style and indenting the query block.

```csharp
var query = @"
                SELECT *
                FROM Products p
                WHERE c.[Category] = 'Electronics'
                JOIN Category c
                ON c.[Category.Id] = p.[Category]
                Order By p.[Category]";
```

When we are using dapper there is a clear flow in the code where you even can read the queries sent to the database.

Grouping everything together in the Application-layer is way more intuitive then using the Onion model where there is a bunch of projects, making reviewing code harder.
One of the downsides to this is code-duplication.

#### Lukes off-topic Trivia

Pink Floyds - Cymbaline sounds very much like Rick & Morty's - [Goodbye Moonman](https://www.youtube.com/watch?v=_UtHmqEJBZI) from the episode "Mortynight Run".
A Great Song I'll tell ya! Wonder if Ryan Elder is a Pink Floyd fan?

Until next time! Wubba lubba dub dub!
