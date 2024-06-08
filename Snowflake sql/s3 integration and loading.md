
```sql 

select current_region();



create stage my_stage;

list @my_stage;
ls @my_stage;


create or replace table uniq_training.staging.credits_internal_stg(
cast string,
crew string,
id string
) cluster by (id);


select count(*) from uniq_training.staging.credits_internal_stg;
-- 45476

select * from uniq_training.staging.credits_internal_stg limit 10;


select * from information_schema.load_history;

-- ACID  
--explain using json 
COPY INTO uniq_training.staging.credits_internal_stg
FROM @my_stage/credits.csv
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"' ESCAPE = '\\' SKIP_HEADER=1)
ON_ERROR=abort 
PURGE=TRUE
;

show stages;


use database uniq_training;
use schema uniq_training.staging;

select * from information_schema.load_history;


GRANT USAGE ON WAREHOUSE compute_wh TO ROLE training_role;

-- GRANT USAGE ON schema uniq_training.staging TO TRAINING_ROLE;
-- GRANT all ON schema uniq_training.staging TO TRAINING_ROLE;
-- --GRANT OWNERSHIP ON SCHEMA uniq_training.staging TO TRAINING_ROLE;

-- GRANT USAGE ON DATABASE uniq_training TO TRAINING_ROLE;
-- GRANT USAGE ON SCHEMA uniq_training.staging TO TRAINING_ROLE;

-- GRANT USAGE ON STAGE uniq_training.staging.my_s3_stg TO TRAINING_ROLE;
-- GRANT ALL ON TABLE uniq_training.staging.credits TO TRAINING_ROLE;
-- GRANT ALL ON TABLE uniq_training.staging.keywords TO TRAINING_ROLE;
-- GRANT ALL ON TABLE uniq_training.staging.MOVIES TO TRAINING_ROLE;
-- GRANT ALL ON TABLE uniq_training.staging.RATINGS TO TRAINING_ROLE;






-- # ACCOUNT ADMIN 
create or replace storage integration my_staging_aws_s3
  type = external_stage
  storage_provider = s3
  storage_aws_role_arn = 'arn:aws:iam::323366134375:role/my-snowflake-external-storage-role'
  enabled = true
  storage_allowed_locations = ('s3://snowflake-filestorage-13855/');


show integrations; 

describe integration my_staging_aws_s3;

--s3://snowflake-filestorage-13855/credits/credits1.csv.gz

select $1,$2,$3,$4 from @my_s3_stg/credits/credits1.csv.gz limit 10;

drop stage my_s3_stg;

create or replace stage my_s3_stg
storage_integration = my_staging_aws_s3
url = 's3://snowflake-filestorage-13855/';

ls @my_s3_stg;

-- 1️⃣ # CREDITS csv load
create or replace table uniq_training.staging.credits(
cast string,
crew string,
id string
) cluster by (id);

select count(*) from uniq_training.staging.credits_internal_stg;
-- 45476

select count(*) from uniq_training.staging.credits;
-- 45474

select * from uniq_training.staging.credits limit 3;

--[{'cast_id': 4, 'character': 'Marty Preston', 'credit_id': '52fe47c0c3a36847f8146573', 'gender': 2
select $1,$2,$3,$4 from @my_s3_stg/credits/credits1.csv.gz limit 3;

truncate table uniq_training.staging.credits;

COPY INTO uniq_training.staging.credits
FROM @my_s3_stg/credits/
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"' ESCAPE = '\\' SKIP_HEADER=1)
ON_ERROR=continue
PURGE=TRUE    --delete
;

select * from uniq_training.staging.credits limit 3;

-- 2️⃣ # KEYWORDS csv load
create or replace table uniq_training.staging.keywords(
id string,
keywords string
) cluster by (id);

COPY INTO uniq_training.staging.keywords
FROM @my_s3_stg/keywords/keywords.csv.gz
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"' ESCAPE = '\\' SKIP_HEADER=1)
;

select * from uniq_training.staging.keywords limit 5;

-- 3️⃣ # LINKS csv load
create or replace table uniq_training.staging.links(
movieId string,
imdbId string,
tmdbId string
) cluster by (movieId);

COPY INTO uniq_training.staging.links
FROM @my_s3_stg/keywords/links.csv.gz
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"' ESCAPE = '\\' SKIP_HEADER=1)
;

select * from uniq_training.staging.links limit 5;

-- 4️⃣ # MOVIES csv load

create or replace table uniq_training.staging.movies(
adult string,
belongs_to_collection string,
budget string,
genres string,
homepage string,
id string,
imdb_id string,
original_language string,
original_title string,
overview string,
popularity string,
poster_path string,
production_companies string,
production_countries string,
release_date string,
revenue string,
runtime string,
spoken_languages string,
status string,
tagline string,
title string,
video string,
vote_average string,
vote_count string
) cluster by (id);

COPY INTO uniq_training.staging.movies
FROM @my_s3_stg/movies/movies.csv.gz
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"' ESCAPE = '\\' SKIP_HEADER=1)
ON_ERROR = CONTINUE
;

select * from uniq_training.staging.movies limit 5;

-- 5️⃣ # RATINGS csv load
create or replace table uniq_training.staging.ratings(
userId string,
movieId string,
rating string,
timestamp string
) cluster by (movieId);

select count(*) from uniq_training.staging.ratings;
truncate table uniq_training.staging.ratings;

COPY INTO uniq_training.staging.ratings
FROM @my_s3_stg/ratings/ratings.csv.gz
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"' ESCAPE = '\\' SKIP_HEADER=1)
;

select * from uniq_training.staging.ratings limit 5;



```