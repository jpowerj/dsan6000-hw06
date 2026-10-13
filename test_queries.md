Old version:

```bash
aws s3 ls s3://dataforgood-fb-data/demographic_csvs/children_under_five/children_under_five_lat_30_lon_-40.csv
```

New version:

```bash
aws s3 cp s3://dataforgood-fb-data/csv/month=2019-06/country=YEM/type=children_under_five/YEM_children_under_five.csv.gz test.csv.gz
```

List countries:

```bash
aws s3 ls s3://dataforgood-fb-data/csv/month=2019-06/
```

---

JRC GHSL

```bash
aws s3 ls --no-sign-request s3://jrc-ghsl/ghs-pop/r2023a/4326/3asec/2025/
```

(~15gb file)

