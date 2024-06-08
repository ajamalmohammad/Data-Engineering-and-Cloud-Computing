
```sql

use warehouse COMPUTE_WH;
use role TRAINING_ROLE;
use schema uniq_training.staging;


select count(*) from uniq_training.staging.credits;

-- explain using json 
CREATE OR REPLACE PIPE uniq_training.staging.mypipe
AUTO_INGEST = TRUE           --autoingest true
  AS
COPY INTO uniq_training.staging.credits
FROM @my_s3_stg/credits/
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"' ESCAPE = '\\' SKIP_HEADER=1)
ON_ERROR=continue
;


show pipes;

desc pipe uniq_training.staging.mypipe;

show stages;

--                       323366134375
-- arn:aws:sqs:us-west-2:533267078010:sf-snowpipe-AIDAXYKJR3N5HVWP7ECN4--IvcT4Nr-dLDPWp2wQzWfA


```