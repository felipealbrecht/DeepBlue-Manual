# Working with the data

select_regions — Selects experiment regions matching the given parameters
select_annotations — Selects annotation regions matching the given parameters

count_regions — Counts the number of regions in the result of the given query

get_experiments_by_query - Gets the regions for the given query in the requested BED format

filter_regions — Filters the result of the given query by the given restrictions

intersection — Calculates the intersection of the given queries

merge_queries — Merges the regions of the given queriess

tiling_regions — Creates regions with the tiling size over the chromosomes

get_regions — Gets the regions for the given query in the requested BED format

aggregate — Gets the regions for the given query in the requested BED format

DeepBlue provides 2 operations for selecting data: [select_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-select_annotations) for annotations and [select_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-select_regions) for experiments.

