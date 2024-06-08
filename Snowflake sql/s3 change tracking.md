
```sql
-- # https://docs.snowflake.com/en/sql-reference/constructs/changes

use warehouse compute_wh;
use role TRAINING_ROLE;
use schema uniq_training.staging;


explain using  json
ALTER TABLE uniq_training.staging.credits SET CHANGE_TRACKING = TRUE;

select count(*) from uniq_training.staging.credits;


```