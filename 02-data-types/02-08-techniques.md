## Techniques

The technique data type contains information on experimental techniques thereby refining the epigenetic mark annotation.
The technique controlled vocabulary contains the technique name and its description.

The command [list_techniques](http://deepblue.mpi-inf.mpg.de/api.html#api-list_techniques) lists all techniques included into DeepBlue:

```python
>>> print s.list_techniques(uk)
['okay', [['t1', 'RRBS'], ['t2', 'Infinium 450k'], ['t3', 'BisulfiteSeq'], ['t4', 'ChipSeq'], ['t5', 'ChipSeq Uniform'], ['t6', 'DNaseSeq'], ['t7', 'DNaseSeq Uniform'], ['t8', 'Chromatin State Segmentation by HMM'], ['t9', 'RNASeq']]]
```

Similar techniques names can be found using [list_similar_techniques](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_techniques)

The command [add_technique](http://deepblue.mpi-inf.mpg.de/api.html#api-add_technique) is used to insert a technique.
Note that not all users have permissions to add new techniques.
