## Listing

[DeepBlue API](http://deepblue.mpi-inf.mpg.de/api.html) provides a set of listing methods.
Each [data types](../02-data-types/02-00-data-types.md) has a ```list``` and ```list_similar``` operations.
All listing operations return a set of id and names, with exception the samples, that return a set of id and a key-value table.
It is possible to read the [data identifier](03-03-data-identifier.md) using the command [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info).

The [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments) can list the Experiments by Genome, epigenetic_mark, sample, technique, project, or all projects. It does accept any combination of the parameters, where the parameters can be used to filter the selection.
For instance, without any filter, the [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments) returns all the Experiments inserted into DeepBlue.

The [list_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-list_annotations) requires the Genome name as parameter because the same Annotation name can be used for different Genomes, for instance, Genes locations.

The ```list_similar``` commands list all elements from the controlled vocabulary that are similar with the given input. The list_similar is available for
 [Experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_experiments), [Genomes](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_genomes), [Epigenetic Marks](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_epigenetic_marks), [BioSources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_bio_sources), [Projects](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_projects), and [Techniques](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_techniques).
