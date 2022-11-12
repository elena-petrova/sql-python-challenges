*Optimised (read "better") solutions for the subset of questions from [Top 30 Python Interview Questions and Answers](https://www.stratascratch.com/blog/top-30-python-interview-questions-and-answers/).*
## ID 10019: Find the probability of rides for each weather and the hour
Difficulty: Medium

[Source](https://platform.stratascratch.com/coding/10019-find-the-probability-of-ordering-a-ride-based-on-the-weather-and-the-hour?code_type=2)


- Find the probability of total rides each weather-hour combination constitutes.
- Output the weather, hour along with the corresponding probability.
- Sort records by the weather and the hour in ascending order.

```python
import pandas as pd

lyft_rides.shape[0]
lyft_rides['probability'] = lyft_rides.groupby(['weather', 'hour'])['index'].transform('count')/lyft_rides.shape[0]
lyft_rides[['weather', 'hour', 'probability']].sort_values(['weather', 'hour'], ascending=True).drop_duplicates()
```

## ID 2001: Share of Loan Balance

Difficulty: Medium

[Source](https://platform.stratascratch.com/coding/2001-share-of-loan-balance?code_type=2)

- Write a query that returns the rate_type, loan_id and balance of each loan type.
- Add a column that shows with what % the loan's balance contributes to the total balance among the loans of the same rate type.

```python
import pandas as pd

submissions['loan_share'] = submissions['balance']/submissions.groupby('rate_type')['balance'].transform('sum') * 100
submissions[['rate_type', 'loan_id', 'balance', 'loan_share']].sort_values('loan_share', ascending=False)
```

## ID 9610: Find students with a median writing score

Difficulty: Hard (?)

[Source](https://platform.stratascratch.com/coding/9610-find-students-with-a-median-writing-score?code_type=2)

- Output ids of students with a median score from the writing SAT.

```python
import pandas as pd

sat_writing_median = sat_scores['sat_writing'].median()
list(sat_scores.query('sat_writing == @sat_writing_median')['student_id'])
```

## ID 9895: Duplicate Emails

Difficulty: Easy

[Source](https://platform.stratascratch.com/coding/9895-duplicate-emails?code_type=2)

- Find all emails with duplicates.

```python
import pandas as pd

employee[employee.duplicated(subset=['email'])]
```

## ID 9614: Find the average difference between booking and check-in dates

Difficulty: Medium

[Source](https://platform.stratascratch.com/coding/9614-find-the-average-difference-between-booking-and-check-in-dates?tabname=question)

- Find the average number of days between the booking and check-in dates for AirBnB hosts.
- Order the results based on the average number of days (avg_days_between_booking_and_checkin) in descending order.

```python
import pandas as pd

airbnb_contacts['days_between_booking_and_checkin'] = (
    (airbnb_contacts['ds_checkin'] - airbnb_contacts['ts_booking_at'])
        .dt.days
        .fillna(0)
    )

(airbnb_contacts 
    .groupby('id_host')
    .agg(avg_days_between_booking_and_checkin=('days_between_booking_and_checkin', 'mean'))
    .reset_index()
    .sort_values('avg_days_between_booking_and_checkin', ascending=False)
)
```
