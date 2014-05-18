## Filtering Regions

It is possible to filter the regions using the [filter_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-filter_regions) command. This command receives a query id, the region field name that will be filtered, the operation (```==```, ```=!```, ```>```,```>=```, ```<```, ```<=``), and the field type.

Example:
```python
(status, filtered) = server.filter_regions(query_id, "SCORE", ">","5", "integer", user_key)
print server.count_regions(filtered, user_key)
```

```python
['okay', 1007799]
```