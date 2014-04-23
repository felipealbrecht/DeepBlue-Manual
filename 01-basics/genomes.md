#### Genomes

The genomes controlled vocabulary is genomes assemblies, with the names, descriptions, and chromosome names and sizes.
Now DeepBlue has only genome *hg19* inserted in this database. A new genome assemblies can be easily inserted with the [add_genome](http://deepblue.mpi-inf.mpg.de/api.html#api-add_genome) command, as the following example shows:

```python
genome_data = """chr1 1000000
chr2 900000
chr3 500000
chrX 100000"""
print server.add_genome("hgX", "Example of Genome for the Manual", genome_data, user_key)
``` 
Be aware that only some users have permissions to insert a genome into DeepBlue.

The command [chromosomes](http://deepblue.mpi-inf.mpg.de/api.html#api-chromosomes) list all the chromosomes and theirs sizes of a given genome assembly:
```python
print server.chromosomes("Genome Example", user_key)
```

Uploading the genomic sequences is also possible. It can be made by the [uploada_chromosome](http://deepblue.mpi-inf.mpg.de/api.html#api-upload_chromosome) command:

```python
# Example sequence!
data = "ACTGACTGCG" * 100000 
print server.upload_chromsome("Genome Example", "chr1", data, user_key)
```
In the data retrieval chapter will be discussed how to access and use the chromosome sequences.



A list of all possible commands on Genomes is available in the [DeepBlue - Genome Commands API](http://deepblue.mpi-inf.mpg.de/api.html#api-genomes)