## Free Text Search

The listing operations are useful to find the right name, but they do not look into the content of the data types.
For instance, it is necessary to use the [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) with the correct metadata content to find the expected sample. 
In this way, finding a sample without knowing the metadata content can be a slow task.
We provide the command [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) for simplify the data finding task.

The [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) accepts free text and search the for these text in the data types metadata. 
The first parameters is a free text, for example: "blood cancer". The second parameters is where the search can be made: annotations, bio_sources, epigenetic_marks, experiments, genomes, projects, samples, samples fields, techniques, and tilings. Multiple data types can be placed together.
The result is a set of tuples containing the data id, data name type, and data type.  
The results are ordered by relevance, that is the number of matches between the text input and the data values.
The [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) returns at maximum 100 values.

In the following example, we search for all samples that contains the words "cancer" or "blood" in their description. 
```python
server.search("cancer blood", "samples", user_key)
```

Similar approach can be made to search all Experiments that contains "cancer" or "blood":
```python
server.search("cancer blood", "experiments", user_key)
```

More complexes searchers can be performed.
 * The hyphen symbol (-) can be used to negate a word.
 * Phases can be matched enclosing them in a escaped double quotes(\").


For example, to search for methylation in the epigenetic marks:
```python
server.search("methylation -histone -modification", "epigenetic_marks", user_key)
```

For searching "methylation" AND "cancer" AND NOT "histone" AND NOT "modification":
```python
server.search("\"methylation\" \"cancer\" -rrbs -histone -modification ", "experiments", user_key)
```
Be aware that the terms inside  ```\" \"``` are searched exactly how they appear, turning off the functionality to return similar terms.