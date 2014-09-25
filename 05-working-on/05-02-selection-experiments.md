## Selecting Experiments

The [select_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) command is used to access the experiments' data.
The [select_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) command is similar to [select_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-select_annotations). The difference is that [select_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) accepts ```epigenetic_mark```, ```sample```, ```technique```, and ```project``` parameters.


### Selecting Experiments Example


*Example:*
Firstly, we use the [get_bio_source_related](http://deepblue.mpi-inf.mpg.de/api.html#api-get_bio_source_related) command to retrieve all biosources related to the term "blood" and then we select only the biosources names from the ```blood_related``` list.
Them, we select all samples that use these biosources and get their IDs.
Finally, we select all ```chromosome``` *chr1* regions from the experiments that have ```genome``` *hg19*, ```epigenetic_mark``` *methylation* and the found samples and print the chromosome, start, and end of these regions:

```python
(status, blood_related) = server.get_bio_source_related("blood", user_key)
blood_related_names = [x[1] for x in blood_related]
(status, blood_samples) = server.list_samples(blood_related_names, {"karyotype":"cancer"}, user_key)
blood_samples_ids = [x[0] for x in blood_samples]
(status, query_id) = server.select_regions(None, "hg19", "Methylation", blood_samples_ids, None, None, "chr1", None, None, user_key)
(status, regions) = server.get_regions(query_id, "CHROMOSOME, START, END", user_key)
print regions
```