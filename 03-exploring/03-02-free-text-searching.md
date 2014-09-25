## Free Text Search

The listing operations are useful for listing the IDs and names, but not for searching through data content.
For example, if we wish to search for an [Experiment](../02-data-types/02-01-experiments.md) with associated metadata, we must [list all the experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments), execute [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) and analyze the result of each experiment.
Also, the [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) command needs the correct metadata content to find the expected sample.
In short, it is not an optimal way to search data.
The [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) command is the optimal method for data searching in DeepBluebecause it simplifies the task of finding data.

The [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) command has three parameters: the free text for which to do search, the data type (optional), and the *user_key*. The data type defines the collection on which the search will be made.
The available collections are: *annotations*, *biosources*, *epigenetic_marks*, *experiments*, *genomes*, *projects*, *samples*, *sample fields*, *techniques*, *tilings*, and *column_types*. Multiple data types can be combined, i.e., it is possible to search for the term "cancer" in all experiments and samples.
The search command will search for the free text input in all data content.
This means that the command will look at the data name, description, other data type attributes, and also at the extra metadata.

The [search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) command result is a set of tuples, ordered by relevance, containing the data id, data name, and data type. The command returns a maximum of 100 values.
The command returns a set containing the IDs and names; the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command offers more information about the retrieved items.

In the following example, we search for all samples containing either the word "cancer" **or** "blood" in their description:
```python
server.search("cancer blood", "samples", user_key)
```

The following example searches for cancer **or** blood **or** methylation.
This means that an experiment with only the word "methylation" in its metadata will also be returned.
Experiments containing all three given words will have higher scores and will appear before those experiments with only one or two of the given words:
```python
server.search("cancer blood methylation", "experiments", user_key)
```

More complex searches can also be performed:
 * Words that must be in the metadata should be placed in double quotes
 * Text can be exactly matched by enclosing in escaped double quotes, e.g. *"white cells"*
 * The hyphen symbol (*-*) can be used to exclude a word


To search all experiments including "cancer" **and** "blood" ***and*** "methylation":
```python
server.search("\"cancer\" \"blood\" \"methylation\"", "samples", user_key)
```

And, to search for "methylation" **and** **not** "histone" **and** **not** "modification" in the epigenetic marks:
```python
server.search("methylation -histone -modification", "epigenetic_marks", user_key)
```

To search for "methylation" **and** "cancer"  **and** **not** "rrbs" **and** **not** "histone" **and** **not** "modification" in experiments:
```python
server.search("\"methylation\" \"cancer\" -rrbs -histone -modification ", "experiments", user_key)
```

Please be aware that the terms inside  ```\" \"``` are searched for exactly as they are entered, turning off the default functionality of searching for similar terms.


#### More Examples
[Search](http://deepblue.mpi-inf.mpg.de/api.html#api-search) can be used together with the [info](http://deepblue.mpi-inf.mpg.de/api.html#api-info) command:

```
python
(s, result) = server.search("methylation  -histone -modification cancer ", "experiments", user_key)
for r in result[:3]:   # Select first three elements
	print server.info(r[0], user_key)
```

```python
['okay', {'format': 'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES', 'sex': 'F', 'done': '', 'sample_id': 's334', 'karyotype': 'cancer', 'client_address': '127.0.0.1', 'technique': 'RRBS', 'content_format': 'bed', 'genome': 'hg19', 'type': 'experiment', 'description': 'neuroblastoma cell line, treatment: differentiated with retinoic acid, (Biedler, et al. Morphology and Growth, Tumorigenicity, and Cytogenetics of Human Neuroblastoma Cells in Continuous Culture. Cancer Research 33, 2643-2652, November 1973.)', 'bio_source_name': 'SK-N-SH_RA', 'user': 'Populator', 'upload_end': '', 'tier': '3', 'extra_metadata': {'dataVersion': 'ENCODE Jan 2011 Freeze', 'tableName': 'wgEncodeHaibMethylRrbsSknshraUwSitesRep2', 'subId': '2348', 'dccAccession': 'wgEncodeEH001370', 'dateSubmitted': '2010-09-22', 'obtainedBy': 'UW', 'size': '16M', 'grant': 'Myers', 'cell': 'SK-N-SH_RA', 'dataType': 'MethylRrbs', 'replicate': '2', 'treatment': 'None', 'dateUnrestricted': '2011-06-22', 'type': 'bed', 'composite': 'wgEncodeHaibMethylRrbs', 'labExpId': 'SL1628', 'lab': 'HudsonAlpha', 'geoSampleAccession': 'GSM683919', 'md5sum': '57dcc625654c5e8c32a68836f94ee712', 'project': 'wgEncode', 'epigenetic_mark': 'MethylRrbs', 'view': 'Sites'}, 'lineage': 'ectoderm', 'name': 'wgEncodeHaibMethylRrbsSknshraUwSitesRep2', 'project': 'ENCODE', 'epigenetic_mark': 'Methylation', 'upload_start': '', '_id': 'e57', 'organism': 'human'}]
['okay', {'format': 'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES', 'sex': 'F', 'done': '', 'sample_id': 's334', 'karyotype': 'cancer', 'client_address': '127.0.0.1', 'technique': 'RRBS', 'content_format': 'bed', 'genome': 'hg19', 'type': 'experiment', 'description': 'neuroblastoma cell line, treatment: differentiated with retinoic acid, (Biedler, et al. Morphology and Growth, Tumorigenicity, and Cytogenetics of Human Neuroblastoma Cells in Continuous Culture. Cancer Research 33, 2643-2652, November 1973.)', 'bio_source_name': 'SK-N-SH_RA', 'user': 'Populator', 'upload_end': '', 'tier': '3', 'extra_metadata': {'dataVersion': 'ENCODE Jan 2011 Freeze', 'tableName': 'wgEncodeHaibMethylRrbsSknshraUwSitesRep1', 'subId': '2348', 'dccAccession': 'wgEncodeEH001370', 'dateSubmitted': '2010-09-22', 'obtainedBy': 'UW', 'size': '16M', 'grant': 'Myers', 'cell': 'SK-N-SH_RA', 'dataType': 'MethylRrbs', 'replicate': '1', 'treatment': 'None', 'dateUnrestricted': '2011-06-22', 'type': 'bed', 'composite': 'wgEncodeHaibMethylRrbs', 'labExpId': 'SL863', 'lab': 'HudsonAlpha', 'geoSampleAccession': 'GSM683800', 'md5sum': '1f7cb546e11aef908e90084d8bd8aa51', 'project': 'wgEncode', 'epigenetic_mark': 'MethylRrbs', 'view': 'Sites'}, 'lineage': 'ectoderm', 'name': 'wgEncodeHaibMethylRrbsSknshraUwSitesRep1', 'project': 'ENCODE', 'epigenetic_mark': 'Methylation', 'upload_start': '', '_id': 'e47', 'organism': 'human'}]
['okay', {'format': 'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES', 'sex': 'M', 'done': '', 'sample_id': 's269', 'karyotype': 'cancer', 'client_address': '127.0.0.1', 'technique': 'RRBS', 'content_format': 'bed', 'genome': 'hg19', 'type': 'experiment', 'description': 'prostate adenocarcinoma, "LNCaP clone FGC was isolated in 1977 by J.S. Horoszewicz, et al., from a needle aspiration biopsy of the left supraclavicular lymph node of a 50-year-old caucasian male (blood type B+) with confirmed diagnosis of metastatic prostate carcinoma." - ATCC. (Horoszewicz et al. LNCaP Model of Human Prostatic Carcinoma. Cancer Research 43, 1809-1818, April 1983.)', 'bio_source_name': 'LNCaP', 'user': 'Populator', 'upload_end': '', 'tier': '3', 'extra_metadata': {'dataVersion': 'ENCODE Jan 2011 Freeze', 'tableName': 'wgEncodeHaibMethylRrbsLncapDukeSitesRep1', 'subId': '3159', 'dccAccession': 'wgEncodeEH001406', 'dateSubmitted': '2011-01-06', 'obtainedBy': 'Duke', 'size': '14M', 'grant': 'Myers', 'cell': 'LNCaP', 'dataType': 'MethylRrbs', 'replicate': '1', 'treatment': 'None', 'dateUnrestricted': '2011-10-06', 'type': 'bed', 'composite': 'wgEncodeHaibMethylRrbs', 'labExpId': 'SL787', 'lab': 'HudsonAlpha', 'geoSampleAccession': 'GSM683862', 'md5sum': '9e713c244a69462ff2bd50b88ce0ff19', 'project': 'wgEncode', 'epigenetic_mark': 'MethylRrbs', 'view': 'Sites'}, 'lineage': 'endoderm', 'name': 'wgEncodeHaibMethylRrbsLncapDukeSitesRep1', 'project': 'ENCODE', 'epigenetic_mark': 'Methylation', 'upload_start': '', '_id': 'e38', 'organism': 'human'}]
```

In this example, we search for experiments whose metadata does not contain the term "rrbs":
```python
(s, result) = server.search("methylation -rrbs  -histone -modification cancer ", "experiments", user_key)
for r in result[:3]:   # Select first three elements
	print server.info(r[0], user_key)
```

```
['okay', {'technique': 'Bisulfite-Seq', 'DONOR_HEALTH_STATUS': 'Healthy', 'format': 'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES', 'sample_id': 's784', 'done': '', 'DONOR_REGION_OF_RESIDENCE': 'East Anglia', 'SAMPLE_ID': 'ERS214682', 'client_address': '127.0.0.1', 'DONOR_ETHNICITY': 'NA', 'SPECIMEN_PROCESSING': 'fresh', 'content_format': 'bed', 'DONOR_ID': 'S000RD', 'genome': 'hg19', 'SAMPLE_NAME': 'S000RD54', 'type': 'experiment', 'description': '', 'bio_source_name': 'Monocytes', 'SPECIMEN_STORAGE': 'NA', 'DISEASE': 'None', 'user': 'Populator', 'upload_end': '', 'extra_metadata': {'SPECIMEN_PROCESSING': 'fresh', 'CENTER_NAME': 'CNAG', 'DONOR_HEALTH_STATUS': 'Healthy', 'SAMPLE_ID': 'ERS214682', 'MOLECULE': 'genomic DNA', 'INSTRUMENT_MODEL': 'Illumina HiSeq 2000', 'FILE_MD5': '27dc984729aad107f8ebeec56557aaa6', 'TISSUE': 'Cord blood', 'DONOR_REGION_OF_RESIDENCE': 'East Anglia', 'FILE': 'blueprint/data/homo_sapiens/Cord_blood/S000RD/Monocytes/Bisulfite-Seq/S000RD54.hypo_meth.bs_call.20130415.bed.gz', 'FILE_SIZE': '7013143', 'LIBRARY_STRATEGY': 'Bisulfite-Seq', 'CELL_TYPE': 'Monocytes', 'DONOR_ETHNICITY': 'NA', 'NSC': '-', 'SPECIMEN_STORAGE': 'NA', 'DONOR_ID': 'S000RD', 'EXPERIMENT_ID': 'ERX242609', 'SAMPLE_NAME': 'S000RD54', 'READ_STRAND': '-', 'WITHDRAWN': '-', 'SEQ_RUNS_COUNT': '8', 'READ_QUALITIES': '-', 'DISEASE': 'None', 'STUDY_NAME': 'Bisulfite-Seq', 'STUDY_ID': 'ERP002159', 'DONOR_SEX': 'Male', 'LIBRARY_NAME': '108F_BS', 'INSTRUMENT_PLATFORM': 'ILLUMINA', 'TWIN_PAIR_ID': '-', 'BIOMATERIAL_TYPE': 'Primary Cell', 'RSC': '-', 'FIRST_SUBMISSION_DATE': '02-MAY-2013 13:53:39', 'EXPERIMENT_TYPE': 'DNA Methylation', 'BIOMATERIAL_PROVIDER': 'NIHR Cambridge BioResource', 'LIBRARY_LAYOUT': 'SINGLE', 'DONOR_AGE': '-', 'TYPE': 'BS_HYPO_METH_BED_CNAG'}, 'name': 'S000RD54.hypo_meth.bs_call.20130415', 'DONOR_SEX': 'Male', 'BIOMATERIAL_TYPE': 'Primary Cell', 'project': 'Blueprint Epigenetics', 'BIOMATERIAL_PROVIDER': 'NIHR Cambridge BioResource', 'epigenetic_mark': 'Methylation', 'DONOR_AGE': '-', 'upload_start': '', '_id': 'e2119'}]
['okay', {'technique': 'Bisulfite-Seq', 'DONOR_HEALTH_STATUS': 'Healthy', 'format': 'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES', 'sample_id': 's1250', 'done': '', 'DONOR_REGION_OF_RESIDENCE': 'East Anglia', 'SAMPLE_ID': 'ERS337073', 'client_address': '127.0.0.1', 'DONOR_ETHNICITY': 'NA', 'SPECIMEN_PROCESSING': 'fresh', 'content_format': 'bed', 'DONOR_ID': 'C005VG', 'genome': 'hg19', 'SAMPLE_NAME': 'C005VG51', 'type': 'experiment', 'description': '', 'bio_source_name': 'Macrophage M0', 'SPECIMEN_STORAGE': 'NA', 'DISEASE': 'None', 'user': 'Populator', 'upload_end': '', 'extra_metadata': {'SPECIMEN_PROCESSING': 'fresh', 'CENTER_NAME': 'CNAG', 'DONOR_HEALTH_STATUS': 'Healthy', 'SAMPLE_ID': 'ERS337073', 'MOLECULE': 'genomic DNA', 'INSTRUMENT_MODEL': 'Illumina HiSeq 2000', 'FILE_MD5': 'c9a9f52f57c39806a06fad17b0959a92', 'TISSUE': 'Peripheral blood', 'DONOR_REGION_OF_RESIDENCE': 'East Anglia', 'FILE': 'blueprint/data/homo_sapiens/Peripheral_blood/C005VG/Macrophage_M0/Bisulfite-Seq/C005VG51.hypo_meth.bs_call.20140106.bed.gz', 'FILE_SIZE': '3628942', 'LIBRARY_STRATEGY': 'Bisulfite-Seq', 'CELL_TYPE': 'Macrophage M0', 'DONOR_ETHNICITY': 'NA', 'NSC': '-', 'SPECIMEN_STORAGE': 'NA', 'DONOR_ID': 'C005VG', 'EXPERIMENT_ID': 'ERX353591', 'SAMPLE_NAME': 'C005VG51', 'READ_STRAND': '-', 'WITHDRAWN': '-', 'SEQ_RUNS_COUNT': '14', 'READ_QUALITIES': '-', 'DISEASE': 'None', 'STUDY_NAME': 'Bisulfite-Seq', 'STUDY_ID': 'ERP002159', 'DONOR_SEX': 'Male', 'LIBRARY_NAME': '847G_BS', 'INSTRUMENT_PLATFORM': 'ILLUMINA', 'TWIN_PAIR_ID': '-', 'BIOMATERIAL_TYPE': 'Primary Cell', 'RSC': '-', 'FIRST_SUBMISSION_DATE': '09-DEC-2013 09:51:12', 'EXPERIMENT_TYPE': 'DNA Methylation', 'BIOMATERIAL_PROVIDER': 'NIHR Cambridge BioResource', 'LIBRARY_LAYOUT': 'SINGLE', 'DONOR_AGE': '60 - 65', 'TYPE': 'BS_HYPO_METH_BED_CNAG'}, 'name': 'C005VG51.hypo_meth.bs_call.20140106', 'DONOR_SEX': 'Male', 'BIOMATERIAL_TYPE': 'Primary Cell', 'project': 'Blueprint Epigenetics', 'BIOMATERIAL_PROVIDER': 'NIHR Cambridge BioResource', 'epigenetic_mark': 'Methylation', 'DONOR_AGE': '60 - 65', 'upload_start': '', '_id': 'e2010'}]
['okay', {'technique': 'Bisulfite-Seq', 'DONOR_HEALTH_STATUS': 'Multiple myeloma', 'format': 'NAME,SCORE,STRAND,THICK_START,THICK_END,ITEM_RGB,BLOCK_COUNT,BLOCK_SIZES', 'sample_id': 's451', 'done': '', 'DONOR_REGION_OF_RESIDENCE': '-', 'SAMPLE_ID': 'ERS337609', 'client_address': '127.0.0.1', 'DONOR_ETHNICITY': 'Unknown', 'SPECIMEN_PROCESSING': '-', 'content_format': 'bed', 'DONOR_ID': '25145', 'genome': 'hg19', 'SAMPLE_NAME': 'G204', 'type': 'experiment', 'description': '', 'bio_source_name': 'Plasma cells', 'SPECIMEN_STORAGE': '-', 'DISEASE': 'Multiple myeloma', 'user': 'Populator', 'upload_end': '', 'extra_metadata': {'SPECIMEN_PROCESSING': '-', 'CENTER_NAME': 'CNAG', 'DONOR_HEALTH_STATUS': 'Multiple myeloma', 'SAMPLE_ID': 'ERS337609', 'MOLECULE': 'genomic DNA', 'INSTRUMENT_MODEL': 'Illumina HiSeq 2000', 'FILE_MD5': 'cc378693c91def0da81fd113d4698a0b', 'TISSUE': 'Bone marrow', 'DONOR_REGION_OF_RESIDENCE': '-', 'FILE': 'blueprint/data/homo_sapiens/Bone_marrow/25145/Plasma_cells/Bisulfite-Seq/G204.hyper_meth.bs_call.20140106.bed.gz', 'FILE_SIZE': '23548796', 'LIBRARY_STRATEGY': 'Bisulfite-Seq', 'CELL_TYPE': 'Plasma cells', 'DONOR_ETHNICITY': 'Unknown', 'NSC': '-', 'SPECIMEN_STORAGE': '-', 'DONOR_ID': '25145', 'EXPERIMENT_ID': 'ERX301129', 'SAMPLE_NAME': 'G204', 'READ_STRAND': '-', 'WITHDRAWN': '-', 'SEQ_RUNS_COUNT': '8', 'READ_QUALITIES': '-', 'DISEASE': 'Multiple myeloma', 'STUDY_NAME': 'Bisulfite-Seq', 'STUDY_ID': 'ERP002159', 'DONOR_SEX': 'Male', 'LIBRARY_NAME': '594F_BS', 'INSTRUMENT_PLATFORM': 'ILLUMINA', 'TWIN_PAIR_ID': '-', 'BIOMATERIAL_TYPE': 'Primary cells', 'RSC': '-', 'FIRST_SUBMISSION_DATE': '16-AUG-2013 10:50:09', 'EXPERIMENT_TYPE': 'DNA Methylation', 'BIOMATERIAL_PROVIDER': u"Felipe Prosper,University of Navarra in collaboration with Jose I. Martin-Subero,  Institut d'Investigacions Biom\xe8diques August Pi i Sunyer", 'LIBRARY_LAYOUT': 'SINGLE', 'DONOR_AGE': '50 - 55', 'TYPE': 'BS_HYPER_METH_BED_CNAG'}, 'name': 'G204.hyper_meth.bs_call.20140106', 'DONOR_SEX': 'Male', 'BIOMATERIAL_TYPE': 'Primary cells', 'project': 'Blueprint Epigenetics', 'BIOMATERIAL_PROVIDER': u"Felipe Prosper,University of Navarra in collaboration with Jose I. Martin-Subero,  Institut d'Investigacions Biom\xe8diques August Pi i Sunyer", 'epigenetic_mark': 'Methylation', 'DONOR_AGE': '50 - 55', 'upload_start': '', '_id': 'e2012'}]
```