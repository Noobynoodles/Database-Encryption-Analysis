# Database Encryption Performance Analysis

A DBMS project investigating the performance and storage overhead of
AES-256 column-level encryption in Oracle Database, using Oracle APEX
to run SQL and PL/SQL scripts.

## Project Overview

The project compares plaintext and encrypted user tables across datasets
of 10,000, 20,000 and 30,000 user records, with associated transaction data.

The email column in the encrypted table uses AES-256 encryption.
Tests cover point queries, range queries, joins, email searches, bulk
inserts and updates.

## Technologies

- Oracle Database and Oracle APEX
- SQL and PL/SQL
- AES-256 column-level Transparent Data Encryption (TDE)
- DBMS_SQL and DBMS_UTILITY for test execution and timing

## Repository Contents

| Path | Description |
|------|-------------|
| sql/table_creation.sql | Tables, indexes, dataset loader and measurement procedures |
| sql/10k_datasets.sql | Tests for 10,000 user records |
| sql/20k_datasets.sql | Tests for 20,000 user records |
| sql/30k_datasets.sql | Tests for 30,000 user records |
| sql/results.sql | Queries for summarising recorded measurements |
| results/ | Charts and screenshots of experimental results |
| docs/ | Project report |

## Running the Project

Use a dedicated test schema in an Oracle environment that supports
column-level TDE and has the required encryption configuration,
permissions and storage capacity.

1. Run `sql/table_creation.sql` to create the database objects.
2. Run `sql/10k_datasets.sql`.
3. Run `sql/results.sql` and save the results.
4. Repeat with `sql/20k_datasets.sql` and `sql/30k_datasets.sql`.
5. Review the measurements recorded in the `perf_results` table.

The dataset loader truncates and repopulates the project tables.
Run these scripts only in a test environment.

In Oracle APEX, use SQL Workshop → SQL Scripts to run the scripts.
If `SHOW ERRORS` is unsupported, check compilation errors through
the Object Browser or USER_ERRORS view.

## Measurements

- Recorded execution time for each test
- Average, minimum and maximum execution times
- Allocated table storage in megabytes
- Differences between plaintext and encrypted configurations

## Limitations

- The timer has 10-millisecond resolution, so very short operations
  may be recorded as zero.
- The current timing procedure executes SELECT statements without
  fetching their results. Read timings therefore do not represent
  complete query execution and result retrieval.
- Repeated insert and update tests modify the data between runs.
- The bulk update changes the unencrypted salary column.
- Storage measurements reflect allocated table segments.
- The report records a storage-quota limit during encrypted bulk
  insertion at the 30,000-record scale.

Results describe this experimental setup and should not be treated
as general performance guarantees.

## Author

Tey Tiong Sheng
