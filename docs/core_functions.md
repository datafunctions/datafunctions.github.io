#Core Functions
These functions are discrete, composable data manipulation actions.

They are grouped into similar function sets and are called using the following syntax:

    datafunctions.function_set.function_name(arguments)
    
##`datafunctions.cleanse`
###`label_duplicate_rows`
| Argument | Type | Description |
|:-- |:-- |:-- |
|`source_ref`| `STRING` | `IN` Source table or view reference |
|`destination_view_ref`| `STRING` | `IN` Destination view reference |  |
|`unique_identifiers`| `ARRAY<STRING>` | `IN` Column names with expected unique field combination |


``` SQL
CALL datafunctions.cleanse.label_duplicate_rows (
'project_id.dataset_id.source_name', #source_ref STRING
'project_id.dataset_id.destination_view_name', #destination_view_ref STRING
[] #unique_identifiers ARRAY<STRING>
);
```

**Output:**

A view at `destination_view_ref` with the data in the `source_ref` table or view, and an additional field `duplicate_label`:

| New Column | Value | Description |
|:-- |:-- |:-- |
|`duplicate_label`| `unique` | Row is unique for column values defined in `unique_identifiers` |
|`duplicate_label`| `duplicate` | Row is duplicated for column values defined in `unique_identifiers` |

###`deduplicate`
###`replace_substrings`
    input_string STRING, replace_substring_rules ARRAY<STRUCT<substring STRING, replacement STRING>>, OUT output_string STRING

##`datafunctions.compute`
###`cumulative_sum`
    source_ref STRING, destination_view_ref STRING, value_column STRING, partition_columns ARRAY<STRING>, sort_columns ARRAY<STRING>, cumulative_field_name STRING

###`moving_average`
    source_ref STRING, destination_view_ref STRING, value_column STRING, partition_columns ARRAY<STRING>, sort_columns ARRAY<STRING>, moving_average_days INT64

##`datafunctions.profile`
###`count_column_empty_values`
    source_ref STRING, column_name STRING, OUT empty_column_summary STRUCT<row_count INT64, empty_record_count INT64, empty_record_ratio FLOAT64>

###`count_column_null_values`
    source_ref STRING, column_name STRING, OUT column_null_summary STRUCT<row_count INT64, null_record_count INT64, null_record_ratio FLOAT64>

###`get_column_cardinality`
    source_ref STRING, column_name STRING, OUT column_cardinality INT64

###`get_data_shape`
    source_ref STRING, OUT data_shape STRUCT<column_count INT64, row_count INT64>

##`datafunctions.select`
###`all`
    source_ref STRING, destination_view_ref STRING

###`all_except`
    source_ref STRING, destination_view_ref STRING, except_sql ARRAY<STRING>, where_sql ARRAY<STRING>

###`all_except_where`

###`all_where`
```SQL
CALL datafunctions.select.all_where (
'project_id.dataset_id.source_name', #source_ref STRING
'project_id.dataset_id.destination_view_name', #destination_view_ref STRING
[] #where_sql ARRAY<STRING>
);
```


###`columns_where`
    source_ref STRING, destination_view_ref STRING, columns_sql ARRAY<STRING>, where_sql ARRAY<STRING>

###`custom_where`
    source_ref STRING, destination_view_ref STRING, columns_sql ARRAY<STRING>, custom_columns_sql ARRAY<STRING>, where_sql ARRAY<STRING>

###`sql`
``` SQL 
CALL datafunctions.select.sql (
'project_id.dataset_id.source_name', #source_ref STRING
'project_id.dataset_id.destination_view_name', #destination_view_ref STRING
'', #select_line STRING
[], #columns_sql ARRAY<STRING>
[], #except_sql ARRAY<STRING>
[], #replace_sql ARRAY<STRING>
[], #custom_columns_sql ARRAY<STRING>
[], #where_sql ARRAY<STRING>
[]  #groupby_sql ARRAY<STRING>
);
```

##`datafunctions.transform`
###`fill_in_date_gaps`
``` SQL
CALL datafunctions.transform.fill_in_date_gaps (
'project_id.dataset_id.source_name', #source_ref STRING
'project_id.dataset_id.destination_view_name', #destination_view_ref STRING
'' #date_column STRING
);
```

###`pivot`
``` SQL
CALL datafunctions.transform.pivot (
'project_id.dataset_id.source_name', #source_ref STRING
'project_id.dataset_id.destination_view_name', #destination_view_ref STRING
[], #dimensions ARRAY<STRING>, 
'', #metric STRING, 
'', #pivot_field STRING
'_' #new_column_name_delimiter STRING
);
```



###`unpivot`
    source_ref STRING, destination_view STRING, dimensions ARRAY<STRING>, unpivot_columns ARRAY<STRING>

###`left_join`
    source_ref_left STRING, source_ref_right STRING, destination_view STRING, left_join_fields ARRAY<STRING>, right_join_fields ARRAY<STRING>

###`safe_left_join`
    source_ref_left STRING, source_ref_right STRING, destination_view STRING, left_join_fields ARRAY<STRING>, right_join_fields ARRAY<STRING>

##`datafunctions.utilities`
###`get_columns`
    source_ref STRING, OUT columns_out ARRAY<STRING>

###`get_min_or_max_column_value`
``` SQL
CALL datafunctions.utilities.get_min_or_max_column_value ( 
'', #source_ref STRING
'', #column_name STRING
'MIN/MAX', #min_or_max STRING
VARIABLE, #OUT min_max_value ANY TYPE
'STRING/DATE/INT64/ETC' #output_type STRING
);
```

###`get_unique_column_values`
    source_ref STRING, column_name STRING, OUT column_values ARRAY<STRING>

###`add_row_hash_columns_md5`
    source_ref STRING, destination_view_ref STRING, include_columns ARRAY<STRING>, row_hash_name STRING
    
###`add_row_hash_md5`
    source_ref STRING, destination_view_ref STRING, row_hash_name STRING

###`build_gapless_day_array`
    source_ref STRING, day_column STRING, OUT day_array ARRAY<DATE>


