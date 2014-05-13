## Listing

[DeepBlue API](http://deepblue.mpi-inf.mpg.de/api.html) provides a set of listing methods.
The [data types](../02-data-types/02-00-data-types.md) have list and list_similar operations.
All listing operations return a set of id and names, with exception the samples, that return a set of id and a key-value table.

The [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments) can list the experiments by genome, epigenetic_mark, sample, technique, project, or all projects. It does accept any combination of the parameters, where the parameters can be used to filter the selection.
For instance, without any filter, the [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments) returns more than 4000 experiments.

The [list_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-list_annotations) requires the genome name as parameter because the same annotation can be available for different genomes.

The list_similar commands list all elements from the controlled vocabulary that are similar with the given input. The list_similar is available for
 [experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_experiments), [genomes](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_genomes), [epigenetic marks](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_epigenetic_marks), [bio sources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_bio_sources), [projects](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_projects), and 
 [techniques](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_techniques).