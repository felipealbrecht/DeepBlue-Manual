## Experiments by Query

In a [previous section](05-02-selection-experiments.md), we selected all Experiments that matched a set of parameters. DeepBlue provides the command [get_experiments_by_query](http://deepblue.mpi-inf.mpg.de/api.html#api-get_experiments_by_query) to findout which experiments were selected by the [select_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) command.

```python
>>> (status, experiments) = server.get_experiments_by_query(query_id, user_key)
>>> for experiment in experiments[:5]:
>>>   (status, info) = server.info(experiment[0], user_key)
>>>   print info["name"], info["format"]
wgEncodeHaibMethylRrbsNb4UwSitesRep1 CHROMOSOME,START,END,NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES
wgEncodeHaibMethylRrbsJurkatUwSitesRep1 CHROMOSOME,START,END,NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES
wgEncodeHaibMethylRrbsK562HaibSitesRep2 CHROMOSOME,START,END,NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES
wgEncodeHaibMethylRrbsCmkUwSitesRep1 CHROMOSOME,START,END,NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES
wgEncodeHaibMethylRrbsNb4UwSitesRep2 CHROMOSOME,START,END,NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES
```