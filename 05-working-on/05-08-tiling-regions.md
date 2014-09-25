## Tiling Regions

DeepBlue has an operation for generating [tiling regions](http://deepblue.mpi-inf.mpg.de/api.html#api-tiling_regions):

```python
(s, tiling) = server.tiling_regions(100000, "hg19", None, user_key)
print server.count_regions(tiling, user_key)
```

```python
['okay', 31326]
```