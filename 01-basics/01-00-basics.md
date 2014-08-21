# Basics

The idea behind DeepBlue is providing a central data access hub for large collections of epigenomic data, as well as organizing the data using controlled vocabularies. The data is kept in a central server, where the users access, perform operations on, and finally, transfer only the meaningful data.

DeepBlue Epigenomic Data Server has three fundamental parts:
 * The Data - Experiments and Annotations. Experiments Data are the data from Epigenomics Experiments, i.e. the Methylation data for a given Sample, and the Annotations Data are auxiliar data, i.e. Genes Positions.
 * We organize the [genomes](../02-data-types/genomes.md), [projects](../02-data-types/projects.md), [epigenetic marks](../02-data-types/epigenetic-marks.md), [biosources](../02-data-types/bio-sources.md), and [techniques](../02-data-types/techniques.md) into controlled vocabularies. The BioSources controlled vocabulary contains terms imported from the CL, EFO, and UBERON ontologies.
 * Operations - It is possible to refine the data search parameters, filtering, as well, to aggregate the data, filter by overlap regions, and retrieve the data in a user selected format.

The Epigenomic Data contains the experimental data from the [ENCODE](https://www.genome.gov/encode/), [Roadmap Epigenomic Mapping Consortium](http://www.roadmapepigenomics.org/) , [BLUEPRINT](http://www.blueprint-epigenome.eu/), and [DEEP](http://www.deutsches-epigenom-programm.de/epigenomics/) (soon) projects.

This manual explains DeepBlue's usage fully. From [Accessing DeepbBlue](01-01-access.md), [Creating an user](01-02-creating-user.md), the different [Data Types](../02-data-types/02-00-data-types.md) used by DeepBlue, [Exploring the data](../03-exploring/03-00-exploring.md), [Inserting new data](../04-inserting-data/04-00-inserting.md), and [Working with the data](../05-working-on/05-00-working-with-the-data.md).  All the examples were tested in *Python 2.7*, but they can be easily adapted to others programming language. Along with this manual, we provide a links to the [DeepBlue API Reference Guide](http://deepblue.mpi-inf.mpg.de/api.html) about the current command.
