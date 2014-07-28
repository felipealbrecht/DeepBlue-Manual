# Basics
DeepBlue Epigenomic Data Server has three fundamental parts:
 * Epigenomic Data - Experiments and Annotations #FM: how are these defined?
 * Controlled Vocabularies for Genomes, Projects, Epigenetic Marks, Bio Sources, and Techniques
 * Operations - Database operations: Insertion, Search, Filter, Aggregate, and Retrieve

The principal idea behind DeepBlue is providing a central data access hub for large collections of epigenomic data, as well as organizing the data using controlled vocabularies. 
Here the central idea is that the data is kept at a central server, which a user can access, and perform operations on, finally retrieving transferring the result.

The Epigenomic Data contains the experimental data from the [ENCODE](https://www.genome.gov/encode/), [Roadmap Epigenomic Mapping Consortium](http://www.roadmapepigenomics.org/) , [BLUEPRINT](http://www.blueprint-epigenome.eu/) (soon), and [DEEP](http://www.deutsches-epigenom-programm.de/epigenomics/) (soon) projects.
Controlled vocabulary is used for the main DeepBlue data types: [genomes](../02-data-types/genomes.md), [projects](../02-data-types/projects.md), [epigenetic marks](../02-data-types/epigenetic-marks.md), [bio-sources](../02-data-types/bio-sources.md), and [techniques](../02-data-types/techniques.md). Programmatically accessible operations are used to insert data into DeepBlue, list and search the data, filter the data, aggregate the data, and retrieve the data.

This manual explains DeepBlue's usage: [Creating an user](creating-user.md), [Searching for data](searching.md), Inserting new data, Selecting data, Operating the data, and Retrieving data. The examples given are written in *Python 2.7* but they can be easily adapted to others programming language. Along with this manual, we provide a reference guide with all commands and parameters at [DeepBlue API Documentation](http://deepblue.mpi-inf.mpg.de/api.html).

Epigenomic data is provided at regional as well as base pair resolution.
