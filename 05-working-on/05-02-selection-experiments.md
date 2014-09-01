## Selection Experiments

To [select_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) is used to select the Experiments data. The [select_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) is similar to [select_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-select_annotations). The difference is that [select_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) accepts ```epigenetic_mark```, ```sample```, ```technique```, and ```project```.


### Selecting Experiments example


Example of selecting all Experiments that contains samples. The ```query_id``` will be utilized by the others data operation commands.

```python
(status, blood_related) = server.get_bio_source_related("blood", user_key)
blood_related_names = [x[1] for x in blood_related]

(status, blood_samples) = server.list_samples(blood_related_names, {"karyotype":"cancer"}, user_key)

blood_samples_ids = [x[0] for x in blood_samples]

(status, query_id) = server.select_regions(None, "hg19", "Methylation", blood_samples_ids, None, None, "chr1", None, None, user_key)

(status, info) = server.info(query_id, user_key)
```