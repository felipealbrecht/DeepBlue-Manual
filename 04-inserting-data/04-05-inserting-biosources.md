## Inserting BioSource

The [add_bio_source](http://deepblue.mpi-inf.mpg.de/api.html#api-add_bio_source) requires the ```name```, ```description```, and ```extra_metadata```.


```python
extra_metadata = {"term_url":"http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=BTO&termId=BTO%3A0000099"}
(status, bs_id) = server.add_bio_source("Astrocy", "astrocytes, Astrocy is the same as cell line NH-A", extra_metada, user_key)
```