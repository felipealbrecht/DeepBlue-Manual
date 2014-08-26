## Inserting Epigenetic Mark

The [add_epigenetic_mark](http://deepblue.mpi-inf.mpg.de/api.html#api-add_epigenetic_mark) requires the ```name```and ```description```:

```python
(status, em_id) = server.add_epigenetic_mark("h3k27me3", "Histone H3 (tri-methyl K27). Marks promoters that are silenced by Polycomb proteins in a given lineage; large domains are found at inactive developmental loci.", user_key)
```
