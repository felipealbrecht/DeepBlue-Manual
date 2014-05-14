# Basics
DeepBlue is a data server focus in three main points: 
 * Epigenomic Data - Experiments and Annotations
 * Controlled Vocabularies - Data type names: Genomes, Projects, Epigenetic Marks, Bio Sources, and Techniques
 * Operations - operations in the database: Insertion, Search, Filter, Aggregate, and Retrieve

The main benefit from DeepBlue is having all epigenomic data from the major projects in one place, where all the data is organized using controlled vocabularies and the data retrieval process is eased by a set of operations.

The Epigenomic Data contains the experiments data from [ENCODE](https://www.genome.gov/encode/), [Roadmap Epigenomic](http://www.roadmapepigenomics.org/) , [BLUEPRINT](http://www.blueprint-epigenome.eu/) (soon), and [DEEP](http://www.deutsches-epigenom-programm.de/epigenomics/) (soon) Epigenomic Projects.
The controlled vocabulary is used to name the main DeepBlue data types: [genomes](../02-data-types/genomes.md), [projects](../02-data-types/projects.md), [epigenetic marks](../02-data-types/epigenetic-marks.md), [bio-sources](../02-data-types/bio-sources.md), and [techniques](../02-data-types/techniques.md). The operations are used to insert data into DeepBlue, list and search the data, filter the data, aggregate the data, and retrieve the data.

This manual cover the entire DeepBlue usage: [Creating an user](creating-user.md), [Searching for data](searching.md), Inserting new data, Selecting data, Operating the data, and Retrieving data. The coding examples are written in *Python 2.7* but they can be easily adapted to others programming language. Along with this manual, we provide a reference guide with all commands and parameters at [DeepBlue API Documentation](http://deepblue.mpi-inf.mpg.de/api.html).


Epigenomic data based on regions, peak, and base pair resolution.