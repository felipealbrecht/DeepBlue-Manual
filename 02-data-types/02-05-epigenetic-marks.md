## Epigenetic Marks

The epigenetic mark contains all epigenetic modifications and variations. It includes DNA Methylation, DNaseI hypersensitive sites, mRNA, Histone Variants and Post-translational modification. We also included Chromatin State Segmentation is important for understanding the regulatory process even being not a natural epigenetic mark.

Use the command [list_epigenetic_marks](http://deepblue.mpi-inf.mpg.de/api.html#api-list_epigenetic_marks) to list all epigenetic marks included into DeepBlue:

```python
print server.list_epigenetic_marks(user_key)
``` 

Inserting new epigenetic marks is made using the [add_epigenetic_mark](http://deepblue.mpi-inf.mpg.de/api.html#api-add_epigenetic_marks) command.

```python
print server.add_epigenetic_mark("Epigenetic Mark Example", "A example of epigenetic mark", user_key)
```

Before inserting a new epigenetic_mark, check if a similar name already exists using [list_similar_epigenetic_marks](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_epigenetic_marks):
```python
print server.list_similar_epigenetic_marks("methylation", user_key)
```
This command will return the more similar epigenetic marks names:
```python
['okay', ['Methylation', 'mRNA-seq', 'PAX5-N19', 'H4K12bio', 'eGFP-FOS']]
```
The command [list_similar_epigenetic_marks](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_epigenetic_marks) should be used carefully because it still needs some sensibility adjusts.