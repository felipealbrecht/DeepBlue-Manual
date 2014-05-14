### Example: Obtaining all experiments from from a Bio Source
 
The following code is an example of how to select all samples from the tissue colon:

```python
(s, related) = server.get_bio_source_related("colon", user_key)
related_names = [x[1] for x in related] # get Bio Source names
(s, samples) = server.list_samples(related_names, {}, user_key)
samples_id = [x[0] for x in samples] # get samples id
print server.list_experiments(None, None, samples_id, None, None, uk)
```

```python
['okay', [['e70', 'wgEncodeHaibMethylRrbsHct116StanfordSitesRep1'], ['e187', 'wgEncodeHaibMethylRrbsHct116StanfordSitesRep2'], ['e189', 'wgEncodeHaibMethylRrbsCaco2UwSitesRep1'], ['e262', 'wgEncodeAwgDnaseUwCaco2UniPk'], ['e304', 'wgEncodeAwgDnaseUwHct116UniPk'], ['e336', 'wgEncodeUwHistoneCaco2H3k36me3StdPkRep1'], ['e360', 'wgEncodeUwHistoneCaco2H3k4me3StdHotspotsRep1'], ['e380', 'wgEncodeUwHistoneCaco2H3k27me3StdHotspotsRep2'], ['e411', 'wgEncodeUwHistoneCaco2H3k4me3StdHotspotsRep2'], ['e423', 'wgEncodeUwHistoneCaco2H3k4me3StdPkRep2'], ['e448', 'wgEncodeUwHistoneHct116H3k4me3StdPkRep1'], ['e517', 'wgEncodeUwHistoneCaco2H3k4me3StdPkRep1'], ['e601', 'wgEncodeUwHistoneHct116H3k4me3StdHotspotsRep2'], ['e613', 'wgEncodeUwHistoneHct116H3k4me3StdHotspotsRep1'], ['e625', 'wgEncodeUwHistoneCaco2H3k27me3StdPkRep1'], ['e629', 'wgEncodeUwHistoneCaco2H3k27me3StdPkRep2'], ['e637', 'wgEncodeUwHistoneCaco2H3k36me3StdPkRep2'], ['e662', 'wgEncodeUwHistoneCaco2H3k27me3StdHotspotsRep1'], ['e690', 'wgEncodeUwHistoneCaco2H3k36me3StdHotspotsRep2'], ['e696', 'wgEncodeUwHistoneCaco2H3k36me3StdHotspotsRep1'], ['e713', 'wgEncodeUwHistoneHct116H3k4me3StdPkRep2'], ['e747', 'wgEncodeUwDnaseCaco2HotspotsRep2'], ['e785', 'wgEncodeUwDnaseHct116HotspotsRep1'], ['e940', 'wgEncodeUwDnaseCaco2PkRep2'], ['e945', 'wgEncodeUwDnaseCaco2PkRep1']]]
```
