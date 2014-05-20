# Basics
DeepBlue Epigenomic Data Server has three fundamental parts:
 * Epigenomic Data - Experiments and Annotations
 * Controlled Vocabularies - Data type names: Genomes, Projects, Epigenetic Marks, Bio Sources, and Techniques
 * Operations - operations in the database: Insertion, Search, Filter, Aggregate, and Retrieve

The main benefit from DeepBlue is to have the epigenomic data from the major projects in one place.  
All data is organized using controlled vocabularies and the data retrieval process is eased by a set of operations. 
In other words, the data stay in the server, where can user can perform operations on it, and retrieving only the final result.

The Epigenomic Data are the experiments data from [ENCODE](https://www.genome.gov/encode/), [Roadmap Epigenomic](http://www.roadmapepigenomics.org/) (soon), [BLUEPRINT](http://www.blueprint-epigenome.eu/), and [DEEP](http://www.deutsches-epigenom-programm.de/epigenomics/) (soon) Epigenomic Projects. Controlled vocabularies are collections of names and attributes: [genomes](../02-data-types/genomes.md), [projects](../02-data-types/projects.md), [epigenetic marks](../02-data-types/epigenetic-marks.md), [bio-sources](../02-data-types/bio-sources.md), and [techniques](../02-data-types/techniques.md). The operations are how the data is handled in the data server: insertion, list, search, data, filter, aggregate, and retrieve.

This manual cover the entire DeepBlue usage: [Creating an user](01-02-creating-user.md), [Searching for data](../03-exploring/03-00-exploring.md), [Inserting data](../04-inserting-data/04-00-inserting.md), and [working with the data](../05-working-on/05-00-working-with-the-data.md). The source-code examples are written in *Python 2.7* but they can be adapted to others programming language. Along with this manual, we provide links to the reference guide that contains all commands and parameters. The reference guide is available at [DeepBlue API Documentation](http://deepblue.mpi-inf.mpg.de/api.html).
