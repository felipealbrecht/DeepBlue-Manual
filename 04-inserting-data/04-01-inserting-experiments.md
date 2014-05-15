## Inserting Experiment

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

DeepBlue has the ```Column Types``` data type that is used to solve the BED columns naming problem.

#### Columns Types

DeepBlue provides ```Column Types``` data type for predefining columns names and theirs respective types. They should be used to insert an experiment or annotation. Using ```Column Types``` is simples, only needing to inform the ```Column Type``` name. For example, the format defined by ```"Chromosome:String,Start:Integer,End:Integer,Value:Double:0.0"```can be rewrite by ```CHROMOSOMO,START,END,VALUE```.

A ```Column Types``` must be previously created before being used. Each ```Column Type``` contains the 3 information that were defined directly in the BED format field:

 * ```name``` is the unique identifier, that will be used in the BED file descriptor.
 * ```type``` can be ```string```, ```snteger```, ```double```, ```category```, and ```range```.
 * ```ìgnore_if``` can be used to ignore the column content if its content is lexically the same from the defined in the column type.   

Three commands are available to create insert a column type:
 * [create_column_type_simple](http://deepblue.mpi-inf.mpg.de/api.html#api-create_column_type_simple) - To create a column type with simple types: ```string```, ```ìnteger```, and ```double```.
 ```python
 server.create_column_type_simple("NAME", "The Name!", "-", "string", user_key) 
 server.create_column_type_simple("VALUE", "The Value!", "0.0", "double", user_key)
 server.create_column_type_simple("POSITION", "The Position!", "0", "integer", user_key)
 ```
 * [create_column_type_category](http://deepblue.mpi-inf.mpg.de/api.html#api-create_column_type_category) - To create a column type that accepts a predefined set of values.
```python
 server.create_column_type_simple("STRAND", "Strand!", ".", ["+","-"], user_key) 
 ``
 * [create_column_type_range](http://deepblue.mpi-inf.mpg.de/api.html#api-create_column_type_range) - To create a column type that accepts a value that is in the range. (The value range is inclusive.)
 ```python
 server.create_column_type_range("NORMALIZED_SCORE", "Normalized Score", -1.0, 1.0, user_key)
 ```

As standard, always use capital letters for the ```Column Type``` name. 

As DeepBlue already contains pre-defined column types, hardly be necessary to insert new column types.
Use the command [list_column_types](http://deepblue.mpi-inf.mpg.de/api.html#api-list_column_types) to list all inserted column types:
```python
(s, columns) = server.list_column_types(user_key)
for column in columns:
  print column
```

Rewriting the format 
```
no_chr_start_end,milliDel:Integer:0,milliIns:Integer:0,chromosome:String,start:Integer:0,end:Integer:0,strand:String,repName:String,repClass:String```
using Column Types:

```
no_chr_start_end,MILLI_DEL,MILLI_INS,CHROMOSOME,START,END,STRAND,REP_NAME,REP_CLASS
```

The standard [BED format](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) has the following format in DeepBlue:

```
'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES,BLOCK_STARTS'
```

It is possible to inspect the Experiment format using the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command.
We [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) for all experiments that contains "methylation" and "blood" in their medatada, get their full information using the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command, and print the name and format:

```python
(s, experiments) = server.search("\"methylation\" \"blood\"", "experiments", user_key)
for experiment in experiments:
	(s, e_info) = server.info(experiment[0], user_key)
	print e_info["name"] + " : '" + e_info["format"] + "'"
```
