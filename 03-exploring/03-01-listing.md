## Listing

The [DeepBlue API](http://deepblue.mpi-inf.mpg.de/api.html) provides a set of listing methods.
Each [data type](../02-data-types/02-00-data-types.md) has ```list``` and ```list_similar``` operations.
All listing operations return a set of ids and names, with exception of the samples, which return a set of ids and a key-value table.
It is possible to read the [data identifier](03-03-data-identifier.md) using the command [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info).

The [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments) command lists Experiments by Genome, Spigenetic_mark, Sample, Technique, Project. It accepts any combination of the parameters, allowing users to filter the selection.
For instance, without any filter, [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments) returns all the Experiments in DeepBlue.

The [list_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-list_annotations) command requires the Genome name parameter because the same Annotation name can be used for different Genomes, for example, gene location.

The ```list_similar``` commands list all elements from the controlled vocabulary that are similar to the given input. The ```list_similar``` is available for
 [Experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_experiments), [Genomes](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_genomes), [Epigenetic Marks](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_epigenetic_marks), [BioSources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_bio_sources), [Projects](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_projects), and [Techniques](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_techniques).
