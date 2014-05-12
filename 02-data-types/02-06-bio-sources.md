## Bio Sources and Samples

Bio Sources covers all type of biological source: cell lines, cell types, tissues, organs, and others.
A Bio Source contains a name, description, and extra metadata. The extra metadata is import to include more information about the bio source.

DeepBlue imports Bio Sources from three Ontologies: [Cell type](http://www.ontobee.org/browser/index.php?o=CL), [Experimental Factor Ontology](http://www.ontobee.org/browser/index.php?o=EFO), and [Uber anatomy ontology](http://www.ontobee.org/browser/index.php?o=UBERON). 
For each imported term, together with the name and description is stored the address of a full description of the term, ontology name, namespace of the term, and the ontology comment about the term. 

The command [add_bio_source](http://deepblue.mpi-inf.mpg.de/api.html#api-add_bio_source) is used to insert a Bio Source. It is also possible to list all Bio Sources using the command [list_bio_sources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_bio_sources) and to search all Bio Sources with a similar name thought the command [list_similar_bio_sources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_bio_sources).

DeepBlue implements synonymous for Bio Sources. It means that a Bio Source can be obtained by different names.
A synonymous is set using [set_bio_source_synonym](http://deepblue.mpi-inf.mpg.de/api.html#api-set_bio_source_synonym) command. 
A Bio Source list of synonymous is retrieved by the [get_bio_source_synonyms](http://deepblue.mpi-inf.mpg.de/api.html#api-get_bio_source_synonyms) command:

```python
(s, synonyms) = server.get_bio_source_synonyms("blood", user_key)
```
The ```synonyms``` variable will contain ```['blood', 'portion of blood', 'vertebrate blood']```.

DeepBlue also organizes the Bio Sources in a hierarchy, where we can set terms with a more embracing context over others terms.
The command [set_bio_source_scope](http://deepblue.mpi-inf.mpg.de/api.html#api-set_bio_source_scope) is used to set the scope between two bio sources.
Use the command [get_bio_source_scope](http://deepblue.mpi-inf.mpg.de/api.html#api-get_bio_source_scope) to list the bio sources that are under another bio souces in the bio sources hierarchy.

```python
(s, less_embracing) = server.get_bio_source_scope("blood", user_key)
```
The ```less_embracing``` variable will contain ```['blood', 'portion of blood', 'vertebrate blood']```.


### Samples

Bio Sources are not used directly by experiments, but through samples.
From a data organization perspective, **Samples are Bio Sources with metadata**.
The metadata may contain any kind of information about the source, for instance, but not limited to: organism, laboratory, age, karyotype, cell lineage, strain, date, donor sex, donor ethnicity. The metadata fields are very flexible and it is recommended to include all sample information inside there. We try to include all possible metadata during the samples import process.

The sample metadata fields should be included before using the command [add_sample_field](http://deepblue.mpi-inf.mpg.de/api.html#api-add_sample_field).
It is simple to include a new field with this command, needing the field name, the type (string or numeral), description, and the user key. An error message will be returned if a field with the same name already exists.

The command [add_sample](http://deepblue.mpi-inf.mpg.de/api.html#api-add_sample) is used to include a new sample as well its metadata.
The command [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) list all samples from a given Bio Source, and the command [get_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-get_samples) get samples by the bio_source name and metadata.
