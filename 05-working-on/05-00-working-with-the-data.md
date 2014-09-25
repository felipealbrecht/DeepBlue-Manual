# Working with the Data

DeepBlue has the following commands for working with the data:

* [select_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) — select experiment regions that match the given parameters
* [select_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-select_annotations) — select annotation regions that match the given parameters
* [filter_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-filter_regions) — filter the regions
* [intersection](http://deepblue.mpi-inf.mpg.de/api.html#api-intersection) — return the regions that intersect the regions from another query
* [merge_queries](http://deepblue.mpi-inf.mpg.de/api.html#api-merge_queries) — merge two queries into one
* [tiling_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-tiling_regions) — create regions of the given tiling size over the chromosomes
* [get_experiments_by_query](http://deepblue.mpi-inf.mpg.de/api.html#api-get_experiments_by_query) — return the Experiment names and IDs of the selected regions
* [count_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-count_regions) — count the number of regions
* [get_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-get_regions) — return the query regions
* [aggregate](http://deepblue.mpi-inf.mpg.de/api.html#api-aggregate) — get the regions for the given query in the requested BED format

The usual workflow is to select the data with [select_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) and [select_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-select_annotations).
Next, filter the data with [filter_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-filter_regions) or [intersection](http://deepblue.mpi-inf.mpg.de/api.html#api-intersection).
If necessary, select more data and merge them using the [merge_queries](http://deepblue.mpi-inf.mpg.de/api.html#api-merge_queries).
To view the results; it is possible to get the experiments containing selected data with the [get_experiments_by_query](http://deepblue.mpi-inf.mpg.de/api.html#api-get_experiments_by_query), [count_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-count_regions), or [get_regions](http://deepblue.mpi-inf.mpg.de/api.html#api-get_regions) command (in the BED format), or in a data summary using [aggregate](http://deepblue.mpi-inf.mpg.de/api.html#api-aggregate).

The use of these commands will be explained in the following sections.
