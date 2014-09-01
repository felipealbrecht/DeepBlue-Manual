# Data Types

The Experiments Genomic Regions, which we will now simply call as regions, are the DeepBlue central data.
Every Experiment has a set of regions. These regions contain compulsorily a chromosome, start, and end fields.
Others fields, e.g. region name, scores, strand, etc. are also possible.
DeepBlue allows any number of fields be associated with a region.
The Annotations, that are auxiliary data, are also formed by a set of regions in same way as Experiments.

Every Experiment included in DeepBlue contains at least 6 data fields that are part of the Experiment metadata:
 * Experiment Name
 * Genome Assembly
 * Epigenetic Mark
 * BioSource
 * Project
 * Technique

These fields are organized into [controlled vocabularies](02-03-controlled-vocabulary.md). Controlled vocabularies are collections of unique terms, with information about them. For example, the Genome Assembly Controlled Vocabulary contains the name of all Genomic Assemblies that can be used in Experiment metadata.
Terms can be included and removed from a controlled vocabulary, but not modified.

The next sections explain how Experiments and Annotations are organized, and them go through the DeepBlue Controlled Vocabularies individually.
