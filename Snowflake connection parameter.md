Link: https://wcb60762.snowflakecomputing.com/console
Username: kharthi
Password: 


```
Account: wcb60762
Username: kharthi
Warehouse: COMPUTE_WH
Database: SNOWFLAKE
Schema: ACCOUNT_USAGE
```


# Fake data

```python

import csv
from faker import Faker
import random

fake = Faker()

def generate_fake_data(num_rows):
    data = []
    used_ids = set()
    for _ in range(num_rows):
        unique_id = random.randint(1, 10000)
        while unique_id in used_ids:
            unique_id = random.randint(1, 10000)
        used_ids.add(unique_id)
        name = fake.name()
        data.append((unique_id, name))
    return data

def write_to_csv(filename, data):
    with open(filename, 'w', newline='') as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(['ID', 'Name'])
        writer.writerows(data)

if __name__ == "__main__":
    num_rows = 100  # Change this to the desired number of rows
    filename = 'fake_data.csv'
    fake_data = generate_fake_data(num_rows)
    write_to_csv(filename, fake_data)
    print(f"CSV file '{filename}' generated successfully with {num_rows} rows.")


```

