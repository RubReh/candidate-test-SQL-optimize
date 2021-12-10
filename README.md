# candidate-test-SQL-optimize
Testing SQL and reasoning skills with a real-world problem at Divly


# Background
Divly has a lot of data and one feature we have is keeping track of users' transactions in different crypto currencies. These transactions can then be used in many ways. One such feature is the holdings module which in short uses a table of transactions to keep track the total value of holdings in each currency  day by day. Since there's a lot of data it's important to make the SQL queries to fetch this data fast and efficient. The output of such data could looks something like this:

<img width="681" alt="bild" src="https://user-images.githubusercontent.com/38507268/145571086-6baafacd-d939-4724-9a63-bb6d09dcde41.png">

# Divly's transaction table in MySQL
Below is a highly simplified table of a transactions table. It shows the amount of different currency a user received on different dates. 
Really these are separated by different users, but you can disregard that for the purpose of this test task. In other words, this data already filtered so that it contains one single user's transaction data.

The table contents looks like this:

|id|amount|date|currency|
|---|---|---|---|
|1|2|2021-01-01|sek|
|2|3|2021-01-05|sek|
|3|8|2021-01-06|btc|
|4|8|2021-02-01|btc|


In this test task we'll make a query to calculate the cummulative sums for each currency and date starting from the earliest date (2021-01-01) until the latest date in the table ( 2021-02-01)

# The naive and simple solution (that is not good enough)
As long as you're not restricted to using only MySQL we can loop over dates in a language like python for each date that we're interested in.
A pseudo code approach could look like this:

```python
def calculate_cummulative_sums_by_currency(sum_date)
  
   sql_data=  execute_sql(SELECT SUM(amount), date from transactions where transactions.date < sum_date GROUP BY currency;)
   return sql_data
 ```

Looping that same pseudo code over many dates:

date = '2021-01-01'
end_date = '2021-12-31

```python
while date < end_date:
    sum = calculate_cummulative_sums_by_currency(date)
    do_something_with_sum(sum)
    date = increment_date_by_one_day(date)
 ```

This works but it's too slow if we need a sum for several years of data since we're repeating one query for each date. It's slow firstly because we 
loop it in another backend language than MYSQL so there's a lot of CPU and memory overhead going back and forth between MYSQL and another language. Moreover, the cummulative sum on one date is dependent on the sum of previous dates which mySQL almost certainly can take advantage of whereas making one query per date means we're missing out on that optimization. There's gotta be a way to optimize it by making a query that handles the date for us, don't you think?


# First task:
1. Go to this website and insert the data into a MySQL database: https://onecompiler.com/mysql/3xkwy6vvv
2. Based on the data, make one single MySQL query that gives back a list of **cummulative sums** of the amount column for each currency up until each date in the table. Note, the query must be written for mySQL 8.0 or earlier and not some other dialect of SQL.
3. By one single query it simply means that you cannot use another backend language to run several queries and lump them together like in the naive example, but rather you can aggregate MySQL statements into one query that gives you the output by letting MYSQL to the entire job.

The output should look something like this when you're done:


| currency  |date   |  cummulative_amount |
|---|---|---|
|btc|2021-01-06|8|
|btc|2021-02-01|16|
|sek|2021-01-01|2|
|sek|2021-01-05|5|

  
# Second task:
Now, assuming you have the output that is required by the first task (you can do this task even if you fail to replicate the first task), can you find a way
to fill in the blank dates in between where there are no datapoints in the table.

**For example:** The cummulative sum for btc was 8 on 2021-01-06 in the table, but didn't jump up to 16 until 2021-02-01.
Can you create an output where the blank dates are filled out something like for each currency? If you can't find a way to do it in MYSQL, how would you write an algorithm in python (Pseudo code is fine as well) to do it?


| currency  |date   |  cummulative_amount |
|---|---|---|
|btc|2021-01-06|8|
|btc|2021-01-06|8|
|btc|2021-01-06|8|
|btc|2021-01-06|8|
|btc|2021-01-06|8|
.| | |
. | | |
. | | | 
|btc|2021-02-01|16


What we assess when you show us the solution:
- Reasoning skills in your approach
- How well you understand the problem
- The structure and explanation of your query
- You're ability to find a solution to this problem (using any tools and aids you wish except asking someone else to do the task for you)
- How well you know MySQL and algorithmic thinking.
- Your explanation of your approach and solution


# What you can use:
1. Use this website that can be used as your test MYSQL environment and press `run` to add the example data (whihch is all the data you'll be needing):
2. https://onecompiler.com/mysql/3xkwy6vvv (Ping me if the link stops working and I'll send a new one)
3. Other than this all tools and helps are allowed except for asking someone else to do it.

