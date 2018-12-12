# Basic SQlite Commands

The purpose of this tutorial is to demonstrate how to use basic query commands in SQlite. It goes through each of the most commonly used and important commands and explains how and when to use them. All of the examples in this tutorial will use a Movie table with the columns title, releaseYear, and rating. This tutorial does not cover commands associated with creating database tables, only how to retireve information from them. It is also assumed that the user has already set up SQlite.

[multil-lingual](https://fhdenho.github.io/Basic-SQlite-Commands-lang/)

Here is the table that we will get the data from for the following examples

Title                   | Relase year   | Rating
----------------------- | ------------- | ----------
The Matrix              | 1999          | 3
The Notebook            | 2004          | 2
The Empire Strikes Back | 1980          | G
Return of the Jedi      | 1983          | 4
The Matrix Reloaded     | 2003          | 3


### How to use SELECT

The SELECT statement is the most common SQlite command. It's used to retrieve data from a database, and is often used with the other commands mentioned later in the tutorial. To use the command, you need the name of the table you're getting the information from as well as the column name that the information is in. For example:
	
	> SELECT title
	> FROM Movie;

In this example, "Movie" is the table and "title" is the column that we are getting the data from. The above statement will return all of the movie titles from the Movie table. 
Using the SELECT statement is not too complicated, you just have to know how to use it the correct way. Additionally, if you wanted to select all the data in a table to be returned, you would use:

	> SELECT * FROM Movie;

This will return all data in the Movie table, which includes data from all the columns instead of just the information in the "title" column.

### How to use WHERE

The WHERE command is used to find data that satisfies certain conditions. With a table full of Movie tuples, it could be used to retrieve information about a movie with a certain title without having to look through the whole table manually to find it. This command is never really used by itself. Rather, queries usually start out with either SELECT, UPDATE or DELETE and then WHERE comes after the command to make sure that the data being selected is what the user wants. Despite being an optional part of the query, it’s one of the most useful commands. For an example of how the WHERE command is used, we’ll start out with a simple SELECT statement:

	> SELECT title FROM Movie;

This query would select all of the titles from the Movie table. To be more specific about which titles we want to return, we can combine this query with a WHERE command to return all the titles of movies that satisfy a certain condition:

	> SELECT title FROM Movie
	> WHERE rating = ‘G’;

This command would return all the titles of movies that have a G rating. Additionally, we can use operators like AND, NOT, or OR between the conditions to create even more advanced selections:

	> SELECT title FROM Movie
	> WHERE rating = ‘G’ AND releaseYear = 1980;

This would return the titles of movies that were released in 1980 and were rated G. Keep in mind that there are more operators that can be used with the where command.


### How to use ORDER BY

The ORDER BY command is used to put the results from a query into a specific order. Information returned by queries is put in ascending order by default, but this isn't always what you want. You might want to sort the results from a Movie query by rating or release date, for example. This can be done by using this command. It’s usually placed at the end of the query and can sort results in ascending or descending order. Let’s start out with a simple query that we would like to sort:

	> SELECT title, releaseYear 
	> FROM Movie;

This query would retrieve all of the titles of each movie along with their release dates. However, this information will not be sorted. If we wanted to sort the movies by title, we would use the ORDER BY command like this:

	> SELECT title, releaseYear 
	> FROM Movie 
	> ORDER BY title;

By default the ORDER BY command will sort results in ascending order. If you want to sort the results in descending order then put the keyword DESC after the command. Additionally, if we wanted to sort the movies by title and then by the release year, we would separate the columns with a comma like this:

    > SELECT title, releaseYear 
	> FROM Movie 
	> ORDER BY title ASC, releaseYear DESC;

This query would return the titles and release year from all movies with the titles sorted in ascending order and the release year sorted in descending order. Results from a selection can be sorted by as many columns as you like as long as they’re separated by commas.

### How to use MAX and MIN

The MAX command is used to return the maximum value of something in the column that we need. It is primarily used on columns with numbers in them, like the release years or ratings of movies in the table we are using in the examples. The MAX command will never be at the beginning of the query because we must first use the SELECT command to specify which column we want to find the max value of.
 
To use the command, we will first select the column that we want to find the maximum value in.
 
	> SELECT releaseYear 
	> FROM Movie;
	
This query would select all of the release years from the Movie table. To find the most recent year in the Movie table we can use the MAX command in here to find it for us like this:
 
	> SELECT MAX(releaseYear)
	> FROM Movie;
 
The column name is put into the MAX command and it returns the largest value in the column. Additionally, the MIN command can be used to find the smallest value in a column and it's used in exactly the same way. For example, if we wanted to find the earliest release year in the Movie table, we would use:

	> SELECT MIN(releaseYear)
	> FROM Movie;

### How to use AVG

The AVG command returns the average value in a column given the column name. It is used in a similar way to MAX and MIN, but is used for a different purpose. As with the MAX and MIN commands mentioned before, AVG must be used with the SELECT command. To start out we will start out with a SELECT statement: 

	> SELECT rating 
	> FROM Movie; 

That would lead us to get all the ratings for the movie. If we need to get the average rating for all of them we can use the command AVG to get that. For example we can use it like this:

	> SELECT AVG(rating)
	> FROM Movie; 

The return value of this would be the average rating of all of the movies in the table.

### How to use INSERT INTO

The INSERT INTO command is used when you’re trying to add data into a table. In the table we're using for the in the examples for this tutorial, it'd be used to add new movies to the database. To use the command, you need to first list the column names of the values of the new movie that will be added in to the database. In our example, each movie has a title, release year, and rating, so the first part of the command would look like:

	> INSERT INTO Movie (title, releaseYear, rating)
	
Next, we need to define the values of the new movie we're creating. This is done by using the VALUES command. Please note that the columns and the values for that column need to be in same order. If this is not done then the movie information will not be added into the database correctly, so it's very important to make sure this command is used the right way.
	
	> INSERT INTO Movie(title, releaseYear, rating)
	> VALUES('The Matrix', 1999, 3);

As you can see, we insert the values into the columns specified. This command will add a new movie with the title 'The Matrix', the release year 1999, and a rating of 3. Additionally, you can also add more than one movie at a time by separating the new movies with a comma like this:

	> INSERT INTO Movie(title, releaseYear, rating)
	> VALUES('The Matrix', 1999, 3),
	> 		('The Notebook', 2004, 2);
	
This would add both "The Matrix" and "The Notebook" movies into the database along with their respective information.

### How to use UPDATE

The UPDATE command is used to change existing values in a table to something else. It's used when information on a database needs to be corrected or updated. They are made up of three basic parts. First, the table that needs to be updated has to be selected. This is done by typing UPDATE followed by the table to be updated. For example, if the table is called Movie, the first part of the query would look like

	> UPDATE Movie

Next, we need to specify the columns in which we are changing the data as well as what we are changing the data to. We can do this by typing SET followed by the column name and what the updated value in that column will be. For example, if we wanted to change the rating of the movies in the Movie table to G, the query would now look like

	> UPDATE Movie
	> SET rating = ‘G’;

However, there is more that needs to be done if we only want to update a couple of the movies. The query above would change the ratings of all movies in the table to G, which isn’t usually what we want to do. If we only want to change a couple of the values in the table, we need to specify the qualities of the movies that we want to change. This can be done by using the WHERE command. For example, if each Movie in our database has a title and a rating and we want to update the ratings of the movies with a certain title, the query would be:

	> UPDATE Movie
	> SET rating = ‘G’
	> WHERE title = ‘The Empire Strikes Back’;

This is the basic format for UPDATE queries. More advanced updates like changing the values in more than one column can be made by simply adding more changes under the SET command like this:

	> UPDATE Movie
	> SET rating = ‘G’,
	>     releaseYear = 1980
	> WHERE title = ‘The Empire Strikes Back’;

Both of the changes that are listed would be applied to the movies that satisfy the conditions.

### How to use DELETE FROM

The DELETE FROM command is used to remove information from a table. It is very sensitive, and must be used with caution in order to avoid getting rid of the wrong information. It is highly recommended to try out the command as a SELECT statement before using DELETE in order ti make sure the right data is being selected. You have to know what to put in the WHERE clause or else the wrong data on the table will be deleted. Here’s an example:

	> DELETE FROM Movie WHERE title = ‘The Notebook’;

This will delete all the movies with the title “The Notebook”, taking away all of its values and data leaving no trace of it in the Movie table.
HOWEVER, you can also delete all of the data in a table without deleting the table itself by simply using the following:

	> DELETE FROM Movie;

This will erase all the data from the Movie table without deleting the table. In other words, this will keep an empty table named Movie with no data inside of it.

### How To Use The Standard Query Form

Most queries in sqlite are made up of commands that are used in a specific order. This order is called the standard query form, and it can be thought of as steps that are gone through whenever data needs to be retrieved. We’ll go through the standard form step by step, using the commands that we’ve already gone over. The first step is to select the column names of the table that we want to retrieve the data from with the SELECT command:

	> SELECT columnName

Next, we specify which table we’re getting the information from with the FROM command:

	> SELECT columnName
	> FROM Table

Then, we use the WHERE command to list the conditions of the data that we want to retrieve:

	> SELECT columnName
	> FROM Table
	> WHERE condition1 AND condition2 AND …

And finally, we use the GROUP BY command to put the results in a certain order:

	> SELECT columnName
	> FROM Table
	> WHERE condition1 AND condition2 AND …
	> GROUP BY columnName;

And with that we are done. By using a command in this general form you will be able to retrieve the information you want with relative ease. This concludes the tutorial on basic query commands.


