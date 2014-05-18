## Selecting Annotations

The [select_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-select_annotations) receive the name of one or more annotations, the genome, chromosomes, start, and end positions. Any combination of these parameters is possible.

First example: selecting the CpG Island annotation
```python
(s, cpg_island) = server.select_annotations("Cpg Islands", "hg19", None, None, None, user_key)
```

Only the chromosomes X and Y:
```python
(s, cpg_island) = server.select_annotations("Cpg Islands", "hg19", ["chrX", "chrY"], None, None, user_key)
```


Selecting the hox genes
```python
(s, hox_genes) = server.select_annotations("Genes", "hg19", "chr7", 27130000, 27250000, user_key)
```

The [select_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-select_annotations) return value is an query identifier, that can be used in others operations or to retrieve the data with the [get_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-get_regions) command.