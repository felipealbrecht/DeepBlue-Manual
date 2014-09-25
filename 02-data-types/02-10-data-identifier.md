## Data Identifier

Each datum in DeepBlue possesses a unique *Identifier*.
This identifier is returned in all listing, search, query, and insert operations.
The identifiers can be divided into two parts: the prefix, which is one or two letters,
indicating the data type, and a numeric value.

The following table contains the identifier prefixes and their data type:

| Identifier | Data Type       |
|:----------:|-----------------|
| a          | Annotation      |
| e          | Experiment      |
| g          | Genome          |
| em         | Epigenetic Mark |
| bs         | BioSource      |
| s          | Sample          |
| p          | Project         |
| t          | Technique       |
| q          | Query           |

The [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command is to inspect the identifier content:
```python
server.info("e1", user_key)
```


We can use the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command to view the samples' content:

```python
(s, related) = server.get_bio_source_related("blood", user_key)
related_names = [x[1] for x in related] # get the BioSource names
(s, samples) = server.list_samples(related_names, {}, user_key)
samples_id = [x[0] for x in samples] # get samples ID

for _id in samples_id[:20] : # the first 20 samples
 print  server.info(_id, user_key)
```

```
['okay', {'lineage': 'mesoderm', '_id': 's1', 'description': 'B-lymphocyte, lymphoblastoid, International HapMap Project - CEPH/Utah - European Caucasion, Epstein-Barr Virus', 'bio_source_name': 'GM12878', 'organism': 'human', 'sex': 'F', 'user': 'Populator', 'tier': '1', 'karyotype': 'normal', 'type': 'sample'}]
['okay', {'lineage': 'mesoderm', '_id': 's2', 'description': 'leukemia, "The continuous cell line K-562 was established by Lozzio and Lozzio from the pleural effusion of a 53-year-old female with chronic myelogenous leukemia in terminal blast crises." - ATCC', 'bio_source_name': 'K562', 'organism': 'human', 'sex': 'F', 'user': 'Populator', 'tier': '1', 'karyotype': 'cancer', 'type': 'sample'}]
['okay', {'lineage': 'mesoderm', '_id': 's3', 'description': 'leukemia (UCDavis alternate), "The continuous cell line K-562 was established by Lozzio and Lozzio from the pleural effusion of a 53-year-old female with chronic myelogenous leukemia in terminal blast crises." - ATCC', 'bio_source_name': 'K562b', 'organism': 'human', 'sex': 'F', 'user': 'Populator', 'tier': '1', 'karyotype': 'cancer', 'type': 'sample'}]
['okay', {'lineage': 'mesoderm', '_id': 's18', 'description': 'CD4+ cells isolated from human blood and enriched for naive populations', 'bio_source_name': 'Adult_CD4_naive', 'organism': 'human', 'lab': 'Crawford', 'sex': 'B', 'user': 'Populator', 'tier': '3', 'karyotype': 'normal', 'type': 'sample'}]
['okay', {'lineage': 'mesoderm', '_id': 's19', 'description': 'CD4+ cells isolated from human blood and enriched for Th0 populations', 'bio_source_name': 'Adult_CD4_Th0', 'organism': 'human', 'lab': 'Crawford', 'sex': 'B', 'user': 'Populator', 'tier': '3', 'karyotype': 'normal', 'type': 'sample'}]
```
