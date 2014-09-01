## Get Regions

The command [get_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-get_regions) is used for retrieving the sequences from the server. The command parameters are the ```query_id``` and the ```format```.

The format is the name of the fields that were given in the [add_experiment](http://deepblue.mpi-inf.mpg.de/api.html#api-add_experiment) and [add_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-add_annotation).

First example - Retrieving all regions from chromosome 1, blood as biosource, epigenetic mark methylation, and "karyotype: cancer" in the sample:

```python
(status, blood_related) = server.get_bio_source_related("blood", user_key)
blood_related_names = [x[1] for x in blood_related]

(status, blood_samples) = server.list_samples(blood_related_names, {"karyotype":"cancer"}, user_key)
blood_samples_ids = [x[0] for x in blood_samples]

(status, query_id) = server.select_regions(None, "hg19", "Methylation", blood_samples_ids, None, None, "chr1", None, None, user_key)

(status, regions) = server.get_regions(query_id, "CHROMOSOME,START,END", user_key)

print regions
```

### Metafields

Metafields are fields used to obtain more information about the retrieved region.
It is possible to obtain the length and Experiment name of a given region.
The following table show all metafields that work directly with the regions' Experiment metadata:

| Metafield Name   | Data Type              |
|------------------|------------------------|
| @NAME            | Region Experiment Name |
| @LENGTH          | Region Length          |
| @EPIGENETIC_MARK | Region Epigenetic Mark |
| @PROJECT         | Region Project Name    |
| @BIO_SOURCE      | Region BioSource Name |
| @SAMPLE_ID       | Region Sample ID       |

From the previous example, but now returning the Experiment Name, Length and BioSource Name:

```python
(status, regions) = server.get_regions(query_id, "CHROMOSOME,START,END,@NAME,@LENGTH,@BIO_SOURCE", user_key)
```
