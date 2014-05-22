# Data types

The main DeepBlue data type is the *region*. An experiment or an annotation contains a region set.
For instance, a peak is a region, or in cases of base pair resolution, each genomic region is a region.
[Experiments](02-01-experiments.md) and [annotations](02-02-annotations.md) contain metadata that are used to describe and organize their data. 
The experiments metadata contains: name of the experiment, *genome*, *epigenetic mark*, *sample*, *technique*, and *project*.
These metadata fields are organized into [controlled vocabularies](02-03-controlled-vocabulary.md).
(this is very general. A few details and examples would be nice.)

In the next sections, firstly, we will see how experiments and annotations are organized, and after, we will go through the DeepBlue Controlled Vocabularies.