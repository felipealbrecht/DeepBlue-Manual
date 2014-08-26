## Aggregation

DeepBlue can [aggregate](http://deepblue.mpi-inf.mpg.de/api.html#api-aggregate) groups of regions into bigger regions.
The [aggregate](http://deepblue.mpi-inf.mpg.de/api.html#api-aggregate) needs 3 parameters: `query_data_id`, `query_regions_id`, and the data column name that will be the aggregation pivot	.

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


In the following example we are aggregating the retrieve data into tiling regions of the length 100000, and in the end we remove the aggregated regions that does not contain any region.

```python
(status, blood_related) = server.get_bio_source_related("blood", user_key)
blood_related_names = [x[1] for x in blood_related]

(status, blood_samples) = server.list_samples(blood_related_names, {"karyotype":"cancer"}, user_key)

blood_samples_ids = [x[0] for x in blood_samples]

(status, data_id) = server.select_regions(None, "hg19", "Methylation", blood_samples_ids, None, None, "chr1", None, None, user_key)

(s, regions_id) = server.tiling_regions(100000, "hg19", "chr1", user_key)

(status, aggr_id) = server.aggregate(data_id, regions_id, "SCORE", user_key)

(status, aggr_filter) = server.filter_regions(aggr_id, "@AGG.COUNT", ">", "0", "integer", user_key)

(status, regions) =  server.get_regions(aggr_filter, "CHROMOSOME,START,END,@AGG.MIN,@AGG.MAX,@AGG.MEDIAN,@AGG.MEAN,@AGG.SD,@AGG.COUNT", user_key)
```