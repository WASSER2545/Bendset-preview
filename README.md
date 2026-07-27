# Bendset Preview

Bendset is an anonymized, query-level workload trace collected from a
production Databend Cloud environment. Each record combines Databend Cloud
query-history telemetry with aggregate physical-profile statistics, making the
dataset useful for trace-driven workload characterization, synthesis, and
replay; resource-profile modeling; and exact-query or query-template repetition
analysis.

Privacy-sensitive SQL text and user data are not included. Database and user
identifiers are anonymized, while exact-query and parameterized-query hashes
preserve the ability to study repetition without exposing query text.

## Dataset

The preview dataset is available from
[Google Drive](https://drive.google.com/file/d/1MfaQADhnLEhVjQGH4BM6YI7vkBA8ippC/view?usp=drive_link).

## Features

| Feature | Type | Unit | Description |
|---|---|---|---|
| `query_id` | `VARCHAR` | — | Unique identifier for one query execution. |
| `cpu_time_sum` | `DOUBLE` | ns | Sum of CPU time reported by the query's physical-plan operators. |
| `scan_bytes_from_local_disk_sum` | `DOUBLE` | bytes | Bytes scanned from local disk across physical-plan operators. |
| `scan_bytes_from_data_cache_sum` | `DOUBLE` | bytes | Bytes scanned from the data cache across physical-plan operators. |
| `scan_bytes_from_remote_sum` | `DOUBLE` | bytes | Bytes scanned from remote storage across physical-plan operators. |
| `hash_join_nodes` | `DOUBLE` | count | Number of physical `HashJoin` operators in the query profile. |
| `aggregate_partial_nodes` | `DOUBLE` | count | Number of physical `AggregatePartial` operators in the query profile. |
| `sort_nodes` | `DOUBLE` | count | Number of physical `Sort` operators in the query profile. |
| `produced_rows` | `DOUBLE` | rows | Number of rows produced by the root physical-plan operator. |
| `query_start_time` | `TIMESTAMP WITH TIME ZONE` | timestamp | Time at which the query was submitted or started. |
| `event_time` | `TIMESTAMP WITH TIME ZONE` | timestamp | Time at which the recorded terminal query event occurred. |
| `query_queued_duration_ms` | `DOUBLE` | ms | Time spent waiting in the execution queue. |
| `query_duration_ms` | `DOUBLE` | ms | End-to-end query duration. |
| `query_kind` | `VARCHAR` | — | Statement category, such as `Query`, `Insert`, `Update`, or `CopyIntoTable`. |
| `query_hash` | `VARCHAR` | — | Hash identifying an exact query. |
| `query_parameterized_hash` | `VARCHAR` | — | Hash identifying a parameterized query template. |
| `log_type_name` | `VARCHAR` | — | Terminal log status, such as `Finish`, `Error`, or `Aborted`. |
| `scan_rows` | `DOUBLE` | rows | Number of rows scanned during execution. |
| `scan_bytes` | `DOUBLE` | bytes | Total number of bytes scanned during execution. |
| `scan_io_bytes_cost_ms` | `DOUBLE` | ms | Time attributed to scan I/O. |
| `written_rows` | `DOUBLE` | rows | Number of rows written by the statement. |
| `written_bytes` | `DOUBLE` | bytes | Number of logical bytes written by the statement. |
| `written_io_bytes` | `DOUBLE` | bytes | Number of bytes issued through write I/O. |
| `written_io_bytes_cost_ms` | `DOUBLE` | ms | Time attributed to write I/O. |
| `result_rows` | `DOUBLE` | rows | Number of rows in the query result returned to the client. |
| `result_bytes` | `DOUBLE` | bytes | Size of the query result returned to the client. |
| `peek_memory_usage` | `DOUBLE` | bytes | Reported peak memory usage. The source field name is retained verbatim. |
| `current_database` | `VARCHAR` | — | Anonymized database identifier active for the query. |
| `sql_user` | `VARCHAR` | — | Anonymized user identifier. |
| `node_num` | `BIGINT` | count | Number of execution nodes, representing coarse warehouse size rather than a unique warehouse identity. |

The trace does not contain SQL text, session identifiers, or unique warehouse
identifiers. Source-specific scan counters may also be zero when the underlying
telemetry is unavailable, so they should not be interpreted as cache-hit labels
without an additional validity check.
