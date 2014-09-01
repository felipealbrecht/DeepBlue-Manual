# Basics

The idea behind DeepBlue is to provide a central access hub for large collections of epigenomic data, as well as organizing the data using controlled vocabularies. The data are kept in a central server, where they can be accessed, operated, and  transfered as needed.

DeepBlue Epigenomic Data Server has three main parts:
 * The Data - Experiments and Annotations. Experiments Data are the data from Epigenomics Experiments, e.g. the Methylation data of a given Sample, while the Annotations Data are auxiliary data, e.g. Genes Positions.
 * We organize the [Genomes](../02-data-types/genomes.md), [projects](../02-data-types/projects.md), [epigenetic marks](../02-data-types/epigenetic-marks.md), [biosources](../02-data-types/bio-sources.md), and [techniques](../02-data-types/techniques.md) into controlled vocabularies. The BioSources controlled vocabulary contains terms imported from the CL, EFO, and UBERON ontologies.
 * Operations - It is possible to refine the data search parameters,  aggregate the data, filter by overlap region, and retrieve data in a user selected format.

The Epigenomic Data contains the experimental data from the [ENCODE](https://www.genome.gov/encode/), [Roadmap Epigenomic Mapping Consortium](http://www.roadmapepigenomics.org/), [BLUEPRINT](http://www.blueprint-epigenome.eu/), and (soon) [DEEP](http://www.deutsches-epigenom-programm.de/epigenomics/) projects.

This manual explains DeepBlue's usage fully. From [Accessing DeepbBlue](01-01-access.md), [Creating an user](01-02-creating-user.md), and the different [Data Types](../02-data-types/02-00-data-types.md) used by DeepBlue, to [Exploring the data](../03-exploring/03-00-exploring.md), [Inserting new data](../04-inserting-data/04-00-inserting.md), and [Working with the data](../05-working-on/05-00-working-with-the-data.md).  All the examples were tested in *Python 2.7*, but they can easily be adapted to others programming language. Along with this manual, we provide links to the [DeepBlue API Reference Guide](http://deepblue.mpi-inf.mpg.de/api.html) command specification.
