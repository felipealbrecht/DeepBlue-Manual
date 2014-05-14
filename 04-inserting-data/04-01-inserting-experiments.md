## Inserting Experiments

The [add_experiment](http://deepblue.mpi-inf.mpg.de/api.html#api-add_experiment) uses all controlled vocabularies to fill the inserted experiment metadata. 
The parameter ```name``` should contains the experiment name. The name is unique per user. It means that we can have duplicated experiment names, but from different users. 
The parameters ```genome```, ```epigenetic_mark```, ```technique```, ```project``` should be filled with the respective values names. 

The ```sample``` should contains the sample id. Use [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) or [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) to find the sample id. ```description```is a free text field, where the experiment should be described. Since DeepBlue indexes and search all metadata, the description field does not need to include the metadata values. 

The ```extra_metadata``` is a key-value, where any text can be included. For instance, we use the ```extra_metadata```to included the imported experiments metadata that does not belong to the controlled vocabularies.

The ```data``` field is the experiment data. The data can be in the [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) or [WIG](http://genome.ucsc.edu/FAQ/FAQformat.html#format6) formats. The ```format```field should the describes the data format or contains the "wig" as content, in case of using the [WIG](http://genome.ucsc.edu/FAQ/FAQformat.html#format6).

### BED Data format

When inserting an experiment in [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) format, the  ```format``` parameter should describes the data content. The [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) should use tabs (\t) to separate the fields. 
The format fields separated by comma (,) string, where each field must have a ```name```, ```type```. An optional value, named ```ìgnore_if```, can be used to the a value that should be ignored.

Lets see the following BED file:
```
chr1	0	100	1.0
chr1	100	200	1.2
chr1	200	300	0.0
chr1	400	600	0.2
```

One accepted format is:
```python
format_example_one = "Chromosome:String,Start:Integer,End:Integer,Value:Double:0.0"
```
The ```format_example_one``` defines a [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) format with 4 fields.
We will ignore the content of the field ```Value``` when it be "0.0". 
Important: the field content is firstly analyzed lexically. The ```Value``` content should be "0.0", not just "0" to be ignored.

Even this format is valid, it is not the recommended way to describe this BED file for the DeepBlue.
Firstly, DeepBlue already consider that the 3 initial fields as "chromosome", "start", and "end". 
The user only have to specify, using the field ```no_chr_start_end``` when they are *not* the first elements.

The following BED file, that contains 2 (modified) regions from therepeat_mask annotation:
```
43	0	18	chr19	5918	100	+	(TTAGGG)n	Simple_repeat
161	1	0	chr19	0	719	-	ALR/Alpha	Satellite
```
DeepBlue uses the following format for this file:

```
no_chr_start_end,milliDel:Integer:0,milliIns:Integer:0,chromosome:String,start:Integer:0,end:Integer:0,strand:String,repName:String,repClass:String
```
The chromossome, start, and end must be informed when the field ```no_chr_start_end```is used, otherwise DeepBlue will return an error.

The main problem of these two format is the fields names and types. 
For example, an user can insert an experiment where the ```Value``` is a Integer, 
iwhile another user can insert another experiment where the ```Value``` is a double.
Also, different experiments can have different names for a fields with the same semantic, for instance chromosome, that could be defined as ```chrom```, ```chr```, or ```chromosome```.

For solving the BED columns naming problem we created the "Column Types".

#### Columns Types

DeepBlue provides a set of columns types to be used when inserting an experiment or annotation.

[list_column_types](http://deepblue.mpi-inf.mpg.de/api.html#api-list_column_types) 


```python
(s, columns) = server.list_column_types(user_key)
for column in columns:
  print column
```
