## Intersecting Regions

The command [intersection](http://deepblue.mpi-inf.mpg.de/api.html#api-intersection) selects the regions that intersect with another set of regions.
A good usage is to obtain the regions from experiments that overlap with some annotation, e.g. all sites that overlap with some CpG Island.
The command has as parameters two queries ids: the id of the regions that will be filtered, and the id of the regions that will be used for the filtering. The result is a query of the regions of the first set that overlap with the regions of the second set.

```python
>>> (status, cpg_islands) = server.select_annotations("CpG Islands", "hg19", None, None, None, user_key)
>>> (status, overlaps) = server.intersection(filtered, cpg_islands, user_key)
>>> print server.count_regions(overlaps, user_key)
['okay', 611800]
```
