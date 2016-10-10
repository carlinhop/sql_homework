## SQL Questions

First create a database called fringe_shows
```
  #terminal
  psql
  create database fringe_shows;
  \q
```

Populate the data using the script - fringeshows.sql
```
  #terminal
  psql -d fringe_shows -f fringeshows.sql
```

Using the SQL Database file given to you as the source of data to answer the questions.  Copy the SQL command you have used to get the answer, and paste it below the question, along with the result they gave.


## Section 1

  Revision of concepts that we've learnt in SQL today

  1. Select the names of all users.

    select * from users; 

  2. Select the names of all shows that cost less than £15.

  select name from shows where price <  15;

  3. Insert a user with the name "Val Gibson" into the users table.

  insert into users (name) values ('Val Gibson');

  4. Insert a record that Val Gibson wants to attend the show "Two girls, one cup of comedy".

  insert into shows_users(show_id,user_id) values(12,25);

  5. Updates the name of the "Val Gibson" user to be "Valerie Gibson".

  update users set name = 'Valerie Gibson' where name = 'Val Gibson';

  6. Deletes the user with the name 'Valerie Gibson'.

  delete from  users where name = 'Valerie Gibson';

  7. Deletes the shows for the user you just deleted.

  delete from shows_users  where user_id = 25;


## Section 2

  This section involves more complex queries.  You will need to go and find out about aggregate funcions in SQL to answer some of the next questions.

  9. Select the names and prices of all shows, ordered by price in ascending order.

  select name, price from shows order by price asc;

  10. Select the average price of all shows.

  select avg(price) from shows; 

  11. Select the price of the least expensive show.

  select min(price) from shows;

  12. Select the sum of the price of all shows.

  select sum(price) from shows;

  13. Select the sum of the price of all shows whose prices is less than £20.

  select sum(price) from shows where price < 20;

  14. Select the name and price of the most expensive show.

  select name, price  from shows where price = (select max(price) from shows);

  15. Select the name and price of the second from cheapest show.

  select name, price  from (select name, price from shows order by price asc limit 2) as data where price !=  (select min(price) from shows);

  16. Select the names of all users whose names start with the letter "N".

  select name from users where name like 'N%'                                              ;

  17. Select the names of users whose names contain "er".

  select name from users where name like '%er%'                                            ;

## Section 3

  The following questions can be answered by using nested SQL statements but ideally you should learn about JOIN clauses to answer them.

  18. Select the time for the Edinburgh Royal Tattoo.

  select time from times where id = (select id from shows where name = 'Edinburgh Royal Tattoo') ;

  19. Select the number of users who want to see "Shitfaced Shakespeare".

  select count(*) from shows_users where show_id = (select id from shows where name = 'Shitfaced Shakespeare') ;

  20. Select all of the user names and the count of shows they're going to see

  select name, count(*) as show  from shows_users join users on (shows_users.user_id = users.id) group by name  order by show desc;

  21. SELECT all users who are going to a show at 17:15.

  select name from users join shows_users on (users.id = shows_users.user_id) join times on (shows_users.show_id = times.show_id) where times.time = '17:15';
