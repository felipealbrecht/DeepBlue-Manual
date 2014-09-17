## Inserting Experiment


The Experiments use all controlled vocabularies for their metadata. For this reason, before inserting a new Experiment, please make sure that you have included all parameters required by the [add_experiment](http://deepblue.mpi-inf.mpg.de/api.html#api-add_experiment) command:

 * Name - Experiment name – Unique by user
 * Genome - Genome assembly
 * Epigenetic Mark
 * Sample - Sample id
 * Technique - Technique used by the Experiment
 * Project - Project to which this Experiment belongs
 * Description - Free text field containing a description of the experiment
 * Data - Epigenomic data in BED, BEDGRAPH or WIG format
 * Format - File format description
 * Extra metadata - Extra information in the key-value format. – Use to include metadata that does not belong to any controlled vocabulary.

DeepBlue indexes and performs [searches](http://deepblue.mpi-inf.mpg.de/api.html#api-search) on all metadata, including the experiment name, controlled vocabulary terms, description and extra metadata.

Two very important fields are the ```data``` and ```format```.
The data must be in the [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1), [BEDGRAPH](https://genome.ucsc.edu/goldenPath/help/bedgraph.html), or [WIG](http://genome.ucsc.edu/FAQ/FAQformat.html#format6) format. The ```format```field should state which format is being used. If the data is in *BED* format, the column names must be given. Otherwise, only the format name is needed: `bedgraph` or `wig`.

### BED Data format

When inserting an Experiment in [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) format, the  ```format``` parameter should describe the data content.
The format contains the field names separated by commas (,) where each field must have a ```name``` and ```type```. An optional value, named ```ignore_if```, can be used to the a indicate that should be ignored. Remember that the [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) format uses tabs as field separators.

Let's take at the following BED file:
```
chr1	0	100	1.0
chr1	100	200	1.2
chr1	200	300	0.0
chr1	400	600	0.2
```

An acceptable format is:
```python
format_example_one = "Chromosome:String,Start:Integer,End:Integer,Value:Double:0.0"
```
The ```format_example_one``` defines a [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) format with four fields.
We will ignore the content of the field ```Value``` when it is "0.0".
The field content is first analyzed lexically. The ```Value``` content should read ( just "0" will not be ignored).

Even though this format is valid, it is not the recommended way for describing BED files.
The problems of with this format are the fields' names and types.
For example, one user could insert an experiment whose ```Value``` is an integer,
while a different user might insert another experiment whose the ```Value``` is a double.
Also, different Experiments could have different names for fields with the same semantic, for instance *chromosome*, could be defined as ```chrom```, ```chr```, or ```chromosome```.
To help to resolve the problem of column name ambiguity, DeepBlue has the ```Column Types``` data type.

#### Columns Types

DeepBlue provides the ```Column Types``` data type for predefining column names and their respective types.
They should be used to insert an Experiment or Annotation.
Using ```Column Types``` is simple, requiring only the ```Column Type``` name.
For example, the format defined by ```"Chromosome:String,Start:Integer,End:Integer,Value:Double:0.0"```we can rewrite as ```CHROMOSOMO,START,END,VALUE```.

```Column Types``` must be previously created before being used. Each ```Column Type``` contains the three pieces of information that were defined directly in the BED format field:

 * ```name``` is the unique identifier, that will be used in the BED file descriptor.
 * ```type``` can be ```string```, ```integer```, ```double```, ```category```, or ```range```.
 * ```ignore_if``` can be used to ignore the column content if its content is lexically the same as that defined in the ```column_type``.

Three commands are available to create insert a ```column_type``:
 * [create_column_type_simple](http://deepblue.mpi-inf.mpg.de/api.html#api-create_column_type_simple) - To create a ```column_type``` with simple types: ```string```, ```integer```, and ```double```.
 ```python
 server.create_column_type_simple("NAME", "The Name!", "-", "string", user_key)
 server.create_column_type_simple("VALUE", "The Value!", "0.0", "double", user_key)
 server.create_column_type_simple("POSITION", "The Position!", "0", "integer", user_key)
 ```
 * [create_column_type_category](http://deepblue.mpi-inf.mpg.de/api.html#api-create_column_type_category) - To create a ```column_type`` that accepts a predefined set of values.
```python
 server.create_column_type_simple("STRAND", "Strand!", ".", ["+","-"], user_key)
 ```
 * [create_column_type_range](http://deepblue.mpi-inf.mpg.de/api.html#api-create_column_type_range) - To create a ```column_type`` that accepts a value that lies within a given range. (The value range is inclusive.)
 ```python
 server.create_column_type_range("NORMALIZED_SCORE", "Normalized Score", -1.0, 1.0, user_key)
 ```

For consistency, please always use capital letters for the ```Column Type``` name.

As DeepBlue already contains pre-defined ```column_types```,  it should hardly be necessary to insert new ```column_types```.
Use the command [list_column_types](http://deepblue.mpi-inf.mpg.de/api.html#api-list_column_types) to list all ```column_types``` included in DeepBlue:
```python
(s, columns) = server.list_column_types(user_key)
for column in columns:
  print column
```

For example, the following file format:
```
milliDel:Integer:0,milliIns:Integer:0,chromosome:String,start:Integer:0,end:Integer:0,strand:String,repName:String,repClass:String```

Can be rewritten using ```column_types``` as:

```
MILLI_DEL,MILLI_INS,CHROMOSOME,START,END,STRAND,REP_NAME,REP_CLASS
```

The standard [BED format](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) has the following specification in DeepBlue:

```
'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES,BLOCK_STARTS'
```

It is possible to inspect the Experiment format using the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command.
In the following example, we [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) for all Experiments that contains "methylation" and "blood" in their medatada, get their full information using the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command, and print the name and format:

```python
(s, experiments) = server.search("\"methylation\" \"blood\"", "experiments", user_key)
for experiment in experiments:
	(s, e_info) = server.info(experiment[0], user_key)
	print e_info["name"] + " : " + e_info["format"]
```
