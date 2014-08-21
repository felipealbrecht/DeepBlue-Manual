# Data types

The Experiments Genomic Regions, that by now, we will name as regions, are the DeepBlue central data.
Every experiment has a set of regions. These regions contains compulsorily a chromosome, start, and end.
Others fields, i.e. region name, scores, stand, and so on are also possible.
DeepBlue allows any amount of fields be associated with a regions.
The annotations, that auxiliary data, are also formed by a set of regions in same way as Experiments.

Every Experiment included into DeepBlue contains at least 6 data fields, that are part of the experiment metadata:
 * Experiment Name
 * Genome Assembly
 * Epigenetic Mark
 * Bio-Source
 * Project
 * Technique

These fields are organized into [controlled vocabularies](02-03-controlled-vocabulary.md). Controlled vocabularies are collections of unique terms, with information about them. For example, the Genome Assembly Controlled Vocabulary contains the name of all Genomic Assemblies that can be used in an experiment metadata.
Terms can be included and removed in a controlled vocabulary, but not modified.

The next sections inform how experiments and annotations are organized, and afterwards, it will go individually through the DeepBlue Controlled Vocabularies.
