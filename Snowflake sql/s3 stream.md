

```sql

use warehouse compute_wh;
use role TRAINING_ROLE;
use schema uniq_training.staging;

drop stream uniq_training.staging.credits_stream;
CREATE STREAM uniq_training.staging.credits_stream ON TABLE uniq_training.staging.credits;

create table uniq_training.staging.credits_stream_consumer as 
select * from uniq_training.staging.credits_stream;


```