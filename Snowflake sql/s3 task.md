
```sql
use warehouse compute_wh;
use role TRAINING_ROLE;
use schema uniq_training.staging;


create or replace task task_weekly_ops_report
warehouse = 'compute_wh'
-- SCHEDULE = '60 minute'
--schedule = 'using cron 38 3 * * * America/New_York'
as 
COPY INTO uniq_training.staging.credits
FROM @my_s3_stg/credits/
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"' ESCAPE = '\\' SKIP_HEADER=1)
ON_ERROR=continue
;


-- Execute task priviledge
alter task task_weekly_ops_report resume;


```