## Bio Sources and Samples

Bio Sources covers all type of biological source: cell lines, cell types, tissues, organs, and others.
A Bio Source contains a name, description, and extra metadata. The extra metadata is import to include more information about the bio source.

DeepBlue imports Bio Sources from three Ontologies: [Cell type](http://www.ontobee.org/browser/index.php?o=CL), [Experimental Factor Ontology](http://www.ontobee.org/browser/index.php?o=EFO), and [Uber anatomy ontology](http://www.ontobee.org/browser/index.php?o=UBERON). 
For each imported term, together with the name and description is stored the address of a full description of the term, ontology name, namespace of the term, and the ontology comment about the term. 

The command [add_bio_source](http://deepblue.mpi-inf.mpg.de/api.html#api-add_bio_source) is used to insert a Bio Source. It is also possible to list all Bio Sources using the command [list_bio_sources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_bio_sources) and to search all Bio Sources with a similar name thought the command [list_similar_bio_sources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_bio_sources).

Bio Sources are not used directly by experiments, but through samples.
From a data organization perspective, **Samples are Bio Sources with metadata**.
The metadata may contain any kind of information about the source, for instance, but not limited to: organism, laboratory, age, karyotype, cell lineage, strain, date, donor sex, donor ethnicity. The metadata fields are very flexible and it is recommended to include all sample information inside there. We try to include all possible metadata during the samples import process.

The sample metadata fields should be included before using the command [add_sample_field](http://deepblue.mpi-inf.mpg.de/api.html#api-add_sample_field).
It is simple to include a new field with this command, needing the field name, the type (string or numeral), description, and the user key. An error message will be returned if a field with the same name already exists.

The command [add_sample](http://deepblue.mpi-inf.mpg.de/api.html#api-add_sample) is used to include a new sample as well its metadata.
The command [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) list all samples from a given Bio Source, and the command [get_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-get_samples) get samples by the bio_source name and metadata.
