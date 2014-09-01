## Inserting Experiment


The Experiments use all controlled vocabularies for their metadata. For that, before inserting a new Experiment, make sure that you have parameters required by the [add_experiment](http://deepblue.mpi-inf.mpg.de/api.html#api-add_experiment) command:

 * Name - Experiment name. Unique by user.
 * Genome - Genome assembly
 * Epigenetic Mark
 * Sample - Sample id - Use [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) or [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search)
 * Technique - Technique used by the Experiment
 * Project - Project where this Experiment belongs
 * Description - Free text field where the Experiment should be described
 * Data - epigenomic data in BED, BEDGRAPH, or WIG format.
 * Format - The file format description
 * Extra metadata - Extra information in the key-value format. Use to include metadata that does not belong to any controlled vocabularies.

DeepBlue indexes and perform [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) on all metadata, including the name, controlled vocabulary terms, description and extra metadata.

Two very important fields are the ```data``` and ```format```.
The data must be in the [Bed](http://genome.ucsc.edu/FAQ/FAQformat.html#format1), [BedGraph](https://genome.ucsc.edu/goldenPath/help/bedgraph.html), or [Wig](http://genome.ucsc.edu/FAQ/FAQformat.html#format6) format. The ```format```field should which format are being used. If the data is in*Bed* format, it must inform the file columns, other wise, it just should contain the format name: `bedgraph` or `wig`.

### BED Data format

When inserting an Experiment in [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) format, the  ```format``` parameter should describes the data content.
The format contains the the fields names separated by comma (,) where each field must have a ```name```, ```type```. An optional value, named ```ìgnore_if```, can be used to the a value that should be ignored. Remember that the [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) format use tabs (for separating the fields.

Lets see the following BED file:
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
The ```format_example_one``` defines a [BED](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) format with 4 fields.
We will ignore the content of the field ```Value``` when it be "0.0".
The field content is firstly analyzed lexically. The ```Value``` content should be "0.0", not just "0" to be ignored.

Even this format is valid, it is not the recommended way for describing BED files.
The problem of with this format is the fields names and types.
For example, an user can insert an Experiment where the ```Value``` is a Integer,
while another user can insert another Experiment where the ```Value``` is a double.
Also, different Experiments can have different names for a fields with the same semantic, for instance *chromosome*, that could be defined as ```chrom```, ```chr```, or ```chromosome```.
For helping to solve the column names ambiguity,  DeepBlue has the ```Column Types``` data type.

#### Columns Types

DeepBlue provides ```Column Types``` data type for predefining columns names and theirs respective types. They should be used to insert an Experiment or Annotation. Using ```Column Types``` is simples, only needing to inform the ```Column Type``` name. For example, the format defined by ```"Chromosome:String,Start:Integer,End:Integer,Value:Double:0.0"```can be rewrite by ```CHROMOSOMO,START,END,VALUE```.

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
Use the command [list_column_types](http://deepblue.mpi-inf.mpg.de/api.html#api-list_column_types) to list all column types included into DeepBlue:
```python
(s, columns) = server.list_column_types(user_key)
for column in columns:
  print column
```

Another example:

The following file format
```
milliDel:Integer:0,milliIns:Integer:0,chromosome:String,start:Integer:0,end:Integer:0,strand:String,repName:String,repClass:String```
using Column Types:

can be rewritten as:
```
MILLI_DEL,MILLI_INS,CHROMOSOME,START,END,STRAND,REP_NAME,REP_CLASS
```

The standard [BED format](http://genome.ucsc.edu/FAQ/FAQformat.html#format1) has the following format in DeepBlue:

```
'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES,BLOCK_STARTS'
```

It is possible to inspect the Experiment format using the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command.
In the following example, we [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) for all Experiments that contains "methylation" and "blood" in their medatada, get their full information using the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command, and print the name and format:

```python
(s, experiments) = server.search("\"methylation\" \"blood\"", "experiments", user_key)
for experiment in experiments:
	(s, e_info) = server.info(experiment[0], user_key)
	print e_info["name"] + " : '" + e_info["format"] + "'"
```
