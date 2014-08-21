## Free Text Search

The listing operations are useful for listing the ids and names, but not for searching using the data content.
For instance, when we are searching for a [Experiment](../02-data-types/02-01-experiments.md) that contains some metadata, we have to [list all the experiments]((http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments), for each one, execute the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info), and analyze the result.
with it is necessary to use the [list_samples] with the correct metadata content to find the expected sample.
In short, it is not an optimum way for searching data.
Using the [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) command is the optimum way for data searching in DeepBlue.
It is a command that simplify the data finding task.

The [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) command has three parameters: the free text that will be searched and the data type, that is optional, and the user key. The data type is on which collection the search will be made: annotations, bio_sources, epigenetic_marks, experiments, genomes, projects, samples, samples fields, techniques, and tilings. Multiple data types can be placed together, i.e. it is possible to search by the term "Cancer" in all Experiments and Samples.
The search command will search for the for input free text in all data content. It means that the command will look in the data name, description, others data type attributes, and also the extra metadata.

The [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) command result is a set of tuples, ordered by relevance, containing the data id, data name, and data type. The command returns at maximum 100 values. The command returns a set of id and name, where the command [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info). should be used to retrieve more information about the found items.

In the following example, we search for all samples that contains the words "cancer" **or** "blood" in their description.
```python
server.search("cancer blood", "samples", user_key)
```

The following example searches for cancer **or** blood **or** methylation. That means that experiments with only the work 'methylation' in their metadata can also be returned. Experiments with the three given words will have higher scores and will appear before that experiments with only two or one of the given words.
```python
server.search("cancer blood methylation", "experiments", user_key)
```

More complexes searchers can be performed:
 * Words that must be in the metadata must be inside double quotes
 * Exactly text can be matched enclosing them in a escaped double quotes, i.e. *"white cells"*
 * The hyphen symbol (*-*) can be used to negate a word


For searching all experiments that contains "cancer" **and** "blood" *and* methylation:
```python
server.search("\"cancer\" \"blood\" \"methylation\"", "samples", user_key)
```

For example, to search for methylation in the epigenetic marks:
```python
server.search("methylation -histone -modification", "epigenetic_marks", user_key)
```

For searching "methylation" **and** "cancer" **and** **not** "histone" **and** **not** "modification":
```python
server.search("\"methylation\" \"cancer\" -rrbs -histone -modification ", "experiments", user_key)
```

Be aware that the terms inside  ```\" \"``` are searched exactly how they are given, turning off the functionality to return similar terms.