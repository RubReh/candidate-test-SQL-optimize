# candidate-test-SQL-optimize
Testing SQL and reasoning skills with a real problem at Divly


# Background
Divly has a lot of data and at the heart of keeping track of users' transactions in different crypto currencies is the holdings module
which in short uses a table of transactions to keep track of what a user's holdings in each currency were day by day. Since there's a lot of data it's important to make the SQL queries to fetch this data fast and efficient.

# Divly's transaciton table in MySQL
Below is a highly simplified table of a transactions table. It shows the amount of different currency a user received on different dates. 
Really these are separated by different users, but you can disregard this for the purpose of this test task.

The table contents looks like this:

id|amount|date|currency
1|2|2021-01-01|sek
2|3|2021-01-05|sek
3|8|2021-01-06|btc
4|8|2021-02-01|btc


In this test task we'll make a query to calculate the cummulative sums for each currency and date starting from the earliest date (2021-01-01) until the latest date in the table ( 2021-02-01)

# The naive and simple solution (that is not good enough)
As long as you're not restricted to using only MySQL we can loop over dates in a language like python for each date that we're interested in.
Pseudo code cood look like this:

```python
def calculate_cummulative_sums_by_currency(sum_date)
  
   sql_data=  execute_sql(SELECT SUM(amount) from transactions where transactions.date < sum_date;)
   return sql_data
 ```

Looping pseudo code:

date = '2021-01-01'
end_date = '2021-12-31

```python
while date < end_date:
    sum = calculate_cummulative_sums_by_currency(date)
    do_something_with_sum(sum)
    date = increment_date_by_one_day(date)
 ```
  

