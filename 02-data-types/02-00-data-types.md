# Data types

The main DeepBlue data type is *region*. An experiment or an annotation contains a set of regions.
Examples for regions ar peaks in ChIP-seq experiments, or single basepair regions in the case of SNPs.
[Experiments](02-01-experiments.md) and [annotations](02-02-annotations.md) contain metadata that are used to describe and organize their data. 
The experiments metadata contains the following items: name of the experiment, *genome*, *epigenetic mark*, *sample*, *technique*, and *project*. #FM: make a list out of this
These metadata fields are organized into [controlled vocabularies](02-03-controlled-vocabulary.md).
#FM: this is very general. A few details and examples would be nice

In the next sections,  we will first see how experiments and annotations are organized, and afterwards will go through the DeepBlue Controlled Vocabularies.
