### Example: Workflow

![DeepBlue Epigenomic Data Server](http://deepblue.mpi-inf.mpg.de/imgs/workflow.png)

```python

(status, experiment) = server.select_regions("wgEncodeHaibMethylRrbsLncapAndroDukeSitesRep2", "hg19", None, None, None, None, "chr1", None, None, user_key)

(status, cpg) = server.select_annotations("CpG Islands", "hg19", "chr1", None, None, user_key)

(status, exp_filtered) = server.filter_regions(experiment, "SCORE", ">", "10", "integer", user_key)

(status, intersected) = server.intersection(exp_filtered, cpg, user_key)

(status, exp_H3k4me3) = server.select_regions("wgEncodeUwHistoneJurkatH3k4me3StdPkRep2", "hg19", None, None, None, None, "chr1", None, None, user_key)

(status, final) = server.intersection(intersected, exp_H3k4me3, user_key)

print server.count_regions(final, user_key)
```