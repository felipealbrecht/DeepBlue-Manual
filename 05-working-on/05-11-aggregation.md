## Aggregation

DeepBlue can [aggregate](http://deepblue.mpi-inf.mpg.de/api.html#api-aggregate) groups of regions into bigger regions.
The [aggregate](http://deepblue.mpi-inf.mpg.de/api.html#api-aggregate) needs 3 parameters: ```data id```, ```regions id```, and the pivot of the aggregation.

It is possible to retrieve the aggregation result by the Aggregation Metafield:


| Aggregation Command | Description                |
|---------------------|----------------------------|
| @AGG.MIN            | Regions Min Value          |
| @AGG.MAX            | Regions Min Value          |
| @AGG.MEDIAN         | Regions Median             |
| @AGG.MEAN           | Regions Mean               |
| @AGG.VAR            | Regions Variance           |
| @AGG.SD             | Regions Standard Deviation |
| @AGG.COUNT          | Regions count              |


In the following example we are aggregating the retrieve data into tiling regions of the length 100000:

```python
(status, blood_related) = server.get_bio_source_related("blood", user_key)
blood_related_names = [x[1] for x in blood_related]

(status, blood_samples) = server.list_samples(blood_related_names, {"karyotype":"cancer"}, user_key)

blood_samples_ids = [x[0] for x in blood_samples]

(status, data_id) = server.select_regions(None, "hg19", "Methylation", blood_samples_ids, None, None, "chr1", None, None, user_key)

(s, regions_id) = server.tiling_regions(100000, "hg19", "chr1", user_key)

(status, aggr_id) = server.aggregate(data_id, regions_id, "SCORE", user_key)

print server.get_regions(agg_id, "CHROMOSOME,START,END,@AGG.MIN,@AGG.MAX,@AGG.MEDIAN,@AGG.MEAN,@AGG.SD,@AGG.COUNT")
```