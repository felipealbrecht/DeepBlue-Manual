## Obtaining Regions' Sequences

Just use the metafield ```@SEQUENCE``` for obtaining the regions' sequences:

```python
(status, blood_related) = server.get_bio_source_related("blood", user_key)
blood_related_names = [x[1] for x in blood_related]

(status, blood_samples) = server.list_samples(blood_related_names, {"karyotype":"cancer"}, user_key)

blood_samples_ids = [x[0] for x in blood_samples]
(status, query_id) = server.select_regions(None, "hg19", "Methylation", blood_samples_ids, None, None, "chr1", 1, 1000000, user_key)

(status, regions) = server.get_regions(query_id, "CHROMOSOME,START,END,@SEQUENCE", user_key)

print regions
```
