## Genomes

The controlled vocabulary for genomes contains the assemblies names, descriptions, and chromosome names and sizes.
DeepBlue currently only contains the assembly *hg19*, but new genome assemblies can be easily inserted using the [add_genome](http://deepblue.mpi-inf.mpg.de/api.html#api-add_genome) command. The following code example shows how to insert a new genome assembly [#FM: given chromosome sizes?]:

```python
genome_data = """chr1 1000000
chr2 900000
chr3 500000
chrX 100000"""
print server.add_genome("hgX", "Example of Genome for the Manual", genome_data, user_key)
``` 
Be aware that not all users have permissions to insert a new genome into DeepBlue.

The command [chromosomes](http://deepblue.mpi-inf.mpg.de/api.html#api-chromosomes) list all the chromosomes and theirs sizes for a given genome assembly:
```python
print server.chromosomes("hgX", user_key)
```

The ```add_genome``` command also creates an annotation containing all chromosomes and theirs sizes. The annotation name is the identical to the one of the genome. You can find the annotation using the [list_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-list_annotations):

```python
print server.list_annotations("hgX", user_key)
```

Use the [select_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-select_annotations) and [get_results](http://deepblue.mpi-inf.mpg.de/api.html#api-get_regions) commands for obtaining genome annotation.

```python
(s, chromosomes_annotation) = server.select_annotations("hgX", "hgX", None, None, None, user_key)
(s, regions) = server.get_regions(chromosomes_annotation, "CHROMOSOME,START,END", user_key)
print regions
```
It will print:
```
chr1	0	1000000
chr2	0	900000
chr3	0	500000
chrX	0	100000
```

The commands ```select_annotations``` and ```get_regions``` are further explained in the [Exploring the Data](../03-exploring/03-00-exploring.md) section.  

### Genomic Sequences

DeepBlue also stores genomic sequences that can be used during data analysis and filtering. 
We already included the sequences for ```hg19``` genome assembly chromosomes into DeepBlue.

The [uploada_chromosome](http://deepblue.mpi-inf.mpg.de/api.html#api-upload_chromosome) command is available to upload genomic sequences for others genome assemblies:

```python
# Example sequence!
data = "ACTGACTGCG" * 100000 
print server.upload_chromosome("hgX", "chr1", data, user_key)
```
The [Exploring the Data](../03-exploring/03-00-exploring.md) section discusses how to access and use the chromosome sequences.

A list of all possible commands on Genomes is available in the [DeepBlue - Genome Commands API](http://deepblue.mpi-inf.mpg.de/api.html#api-genomes) description.
