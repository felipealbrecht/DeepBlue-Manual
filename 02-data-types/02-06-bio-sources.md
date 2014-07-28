## Bio Sources and Samples

The bio source dta type covers different types of biological source: cell lines, cell types, tissues, organs, and others.
A Bio Source contains a name, description, and additional metadata.
DeepBlue currently imports terms for possible bio sources from three Ontologies: [Cell type](http://www.ontobee.org/browser/index.php?o=CL), [Experimental Factor Ontology](http://www.ontobee.org/browser/index.php?o=EFO), and [Uber anatomy ontology](http://www.ontobee.org/browser/index.php?o=UBERON).
Each imported term, is stored together with its name and description and address of a full description of the term, ontology name, namespace of the term, and the ontology comment about the term. 

The command [add_bio_source](http://deepblue.mpi-inf.mpg.de/api.html#api-add_bio_source) is used to insert a new bio source. It is also possible to list all bio sources using the command [list_bio_sources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_bio_sources) and to search all bio sources with a similar name through the command [list_similar_bio_sources](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_bio_sources).

DeepBlue supports synonymes for Bio Sources. #FM: explain what a synonym is and what it can be used for.
A synonyme can be set using [set_bio_source_synonym](http://deepblue.mpi-inf.mpg.de/api.html#api-set_bio_source_synonym) command.
A bio source list of synonymes is retrieved by the [get_bio_source_synonyms](http://deepblue.mpi-inf.mpg.de/api.html#api-get_bio_source_synonyms) command:

```python
(s, synonyms) = server.get_bio_source_synonyms("blood", user_key)
```
The ```synonyms``` variable will contain ```['blood', 'portion of blood', 'vertebrate blood']```.

DeepBlue also organizes all available bio sources in a hierarchy.
The command [set_bio_source_scope](http://deepblue.mpi-inf.mpg.de/api.html#api-set_bio_source_scope) is used to set the scope between two Bio Sources. #FM: it is unclear what that means
Use the command [get_bio_source_scope](http://deepblue.mpi-inf.mpg.de/api.html#api-get_bio_source_scope) to list the bio sources that are under another bio souces in the bio sources hierarchy. #FM: please provide more details

```python
(s, less_embracing) = server.get_bio_source_scope("blood", user_key)
```
The ```less_embracing``` content will be: 
```python
['okay', ['blood', 'GM12878', 'K562', 'K562b', 'BC_Leukocyte_UHN00204', 'CD20+', 'CD20+_RO01778', 'CD20+_RO01794', 'CD34+_Mobilized', 'CD4+_Naive_Wb11970640', 'CD4+_Naive_Wb78495824', 'CLL', 'CMK', 'Dnd41', 'GM10248', 'GM10266', 'GM13976', 'GM13977', 'GM20000', 'H0287', 'HL-60', 'hMNC-PB', 'hMNC-PB_0082430.9', 'hMNC-PB_0022330.9', 'hMNC-CB', 'hMNC-CB_9111701.6', 'hMNC-CB_8072802.6', 'Jurkat', 'Loucy', 'Lymphoblastoid_cell_line', 'GM18507', 'GM12801', 'GM18505', 'GM12873', 'GM12872', 'GM19193', 'GM18526', 'GM19099', 'GM19238', 'GM19239', 'GM08714', 'GM06990', 'GM12878-XiMat', 'GM19240', 'GM15510', 'GM10847', 'GM12875', 'GM12874', 'GM12871', 'GM12870', 'GM12813', 'GM12812', 'GM12892', 'GM12891', 'GM18951', 'GM12867', 'GM12868', 'GM12869', 'GM12866', 'GM12864', 'GM12865', 'NB4', 'PBDE', 'PBMC', 'Raji', 'T_cells_CD4+', 'Adult_CD4_Th0', 'Adult_CD4_Th1', 'Cord_CD4_Th1', 'Cord_CD4_Th0', 'Adult_CD4_naive', 'Cord_CD4_naive', 'Th1', 'Th1_Wb33676984', 'Th1_Wb54553204', 'Th17', 'Th2', 'Th2_Wb33676984', 'Th2_Wb54553204', 'Treg_Wb78495824', 'Treg_Wb83319432', '416B', 'A20', 'B-cell_(CD19+)', 'B-cell_(CD43-)', 'BMDM', 'CH12', 'EPC_(CD117+_CD71-_TER119-)', 'Erythrobl', 'G1E', 'G1E-ER4', 'G1E-ER4', 'L1210', 'MEP', 'Megakaryo', 'MEL', 'mG/ER', 'NIH-3T3', 'THelper-Activated', 'T-Naive', 'TReg-Activated', 'TReg', 'umbilical cord blood', 'arterial blood', 'venous blood', 'capillary blood']]
```

The command [get_bio_source_related](http://deepblue.mpi-inf.mpg.de/api.html#api-get_bio_source_related) return all bio sources under the given Bio Source and their synonymes:

```python
(s, related) = server.get_bio_source_related("blood", user_key)
```

The ```related``` content is: 
```python
['okay', [['bs2', 'blood'], ['bs2', 'portion of blood'], ['bs2', 'vertebrate blood'], ['bs1', 'GM12878'], ['bs4', 'K562'], ['bs5', 'K562b'], ['bs65', 'BC_Leukocyte_UHN00204'], ['bs108', 'CD20+'], ['bs109', 'CD20+_RO01778'], ['bs110', 'CD20+_RO01794'], ['bs111', 'CD34+_Mobilized'], ['bs112', 'CD4+_Naive_Wb11970640'], ['bs113', 'CD4+_Naive_Wb78495824'], ['bs116', 'CLL'], ['bs124', 'CMK'], ['bs131', 'Dnd41'], ['bs151', 'GM10248'], ['bs152', 'GM10266'], ['bs173', 'GM13976'], ['bs174', 'GM13977'], ['bs184', 'GM20000'], ['bs185', 'H0287'], ['bs241', 'HL-60'], ['bs248', 'hMNC-PB'], ['bs250', 'hMNC-PB_0082430.9'], ['bs249', 'hMNC-PB_0022330.9'], ['bs251', 'hMNC-CB'], ['bs252', 'hMNC-CB_9111701.6'], ['bs253', 'hMNC-CB_8072802.6'], ['bs332', 'Jurkat'], ['bs340', 'Loucy'], ['bs342', 'Lymphoblastoid_cell_line'], ['bs176', 'GM18507'], ['bs154', 'GM12801'], ['bs175', 'GM18505'], ['bs166', 'GM12873'], ['bs165', 'GM12872'], ['bs180', 'GM19193'], ['bs177', 'GM18526'], ['bs179', 'GM19099'], ['bs181', 'GM19238'], ['bs182', 'GM19239'], ['bs150', 'GM08714'], ['bs149', 'GM06990'], ['bs169', 'GM12878-XiMat'], ['bs183', 'GM19240'], ['bs172', 'GM15510'], ['bs153', 'GM10847'], ['bs168', 'GM12875'], ['bs167', 'GM12874'], ['bs164', 'GM12871'], ['bs163', 'GM12870'], ['bs156', 'GM12813'], ['bs155', 'GM12812'], ['bs171', 'GM12892'], ['bs170', 'GM12891'], ['bs178', 'GM18951'], ['bs160', 'GM12867'], ['bs161', 'GM12868'], ['bs162', 'GM12869'], ['bs159', 'GM12866'], ['bs157', 'GM12864'], ['bs158', 'GM12865'], ['bs361', 'NB4'], ['bs390', 'PBDE'], ['bs392', 'PBMC'], ['bs403', 'Raji'], ['bs419', 'T_cells_CD4+'], ['bs34', 'Adult_CD4_Th0'], ['bs35', 'Adult_CD4_Th1'], ['bs129', 'Cord_CD4_Th1'], ['bs128', 'Cord_CD4_Th0'], ['bs33', 'Adult_CD4_naive'], ['bs127', 'Cord_CD4_naive'], ['bs422', 'Th1'], ['bs423', 'Th1_Wb33676984'], ['bs424', 'Th1_Wb54553204'], ['bs425', 'Th17'], ['bs426', 'Th2'], ['bs427', 'Th2_Wb33676984'], ['bs428', 'Th2_Wb54553204'], ['bs430', 'Treg_Wb78495824'], ['bs431', 'Treg_Wb83319432'], ['bs444', '416B'], ['bs445', 'A20'], ['bs448', 'B-cell_(CD19+)'], ['bs449', 'B-cell_(CD43-)'], ['bs451', 'BMDM'], ['bs454', 'CH12'], ['bs459', 'EPC_(CD117+_CD71-_TER119-)'], ['bs473', 'Erythrobl'], ['bs481', 'G1E'], ['bs482', 'G1E-ER4'], ['bs482', 'G1E-ER4'], ['bs489', 'L1210'], ['bs492', 'MEP'], ['bs495', 'Megakaryo'], ['bs496', 'MEL'], ['bs497', 'mG/ER'], ['bs498', 'NIH-3T3'], ['bs507', 'THelper-Activated'], ['bs508', 'T-Naive'], ['bs509', 'TReg-Activated'], ['bs510', 'TReg'], ['bs5708', 'umbilical cord blood'], ['bs24323', 'arterial blood'], ['bs24323', 'blood in artery'], ['bs24323', 'portion of arterial blood'], ['bs24324', 'venous blood'], ['bs24324', 'blood in vein'], ['bs24324', 'portion of venous blood'], ['bs24325', 'capillary blood'], ['bs24325', 'blood in capillary'], ['bs24325', 'portion of blood in capillary'], ['bs24325', 'portion of capillary blood']]]
```

Some bio sources have duplicated ids. For example ```blood```and ```portion of blood``` have the ```id``` ```bs2```. This happens because ```portion of blood```is a synonym of ```blood```.

[#FM: why do you always capitaliza bio sources? please make them all lower case. Ideally it would be one word: "biosource", even in the API]

### Samples

Bio sources are not used directly by [experiments](02-01-experiments.md), but through *samples*.
From a data organization perspective, **Samples are bio sources with metadata**.
The metadata may contain any kind of information about the source such as organism, laboratory, age, karyotype, cell lineage, strain, date, donor sex, donor ethnicity. The metadata fields are very flexible and it is recommended to include all sample information inside there. We try to include as much metadata as possible during a sample's import process.

The sample metadata fields should be included before using the command [add_sample_field](http://deepblue.mpi-inf.mpg.de/api.html#api-add_sample_field).
The necessary information to create a new field are the field name, the type (string or numeral), description, and the user key. 
An error message will be returned if a field with the same name already exists. #FM: is there again the possiblity to check for similar terms?

The command [add_sample](http://deepblue.mpi-inf.mpg.de/api.html#api-add_sample) is used to include a new sample as well its metadata.
The command [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) list all samples from a given bio source and metadata.
The [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) returns a list of key-value elements, where the key is the sample id, and the elements is the metadata of the sample.

```python
server.list_samples("T_cells_CD4+", {}, user_key)
```
Returns:
```python
['okay', ['s342', {'lineage': 'mesoderm', 'karyotype': 'unknown', 'description': 'Parent cell line for T cells CD4+.', 'bio_source_name': 'T_cells_CD4+', 'lab': 'Crawford', 'sex': 'B', 'user': 'Populator', 'tier': '3', '_id': 's342', 'organism': 'human'}]]
```

The command [list_samples](http://deepblue.mpi-inf.mpg.de/api.html#api-list_samples) can be used to retrieve samples based on their metadata. For instance, to retrieve all samples that have "tier 3" in their metadata:
```python
server.list_samples(None, {"tier":"3"}, user_key) 
```

Attention: not all samples have *tier* in their metadata, it depends direcly from the source where the data was imported.
