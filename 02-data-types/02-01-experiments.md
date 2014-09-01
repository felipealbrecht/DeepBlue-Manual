## Experiments

The Epigenomic data is organized as Experiments in DeepBlue.
Each Experiment is compound by a regions set and associated metadata.

One Experiment has the following metadata:
  * *Name* - Experiment name. Should be unique.
  * *Genome* - Genome assembly used by this Experiment. More details in the [Genomes](02-04-genomes.md) section.
  * *Epigenetic mark* - Epigenetic mark of the Experiment. For example: Methylation or some Histone Modification. More details in the [Epigenetic Marks](02-05-epigenetic-marks.md) section.
  * *Sample* - Identification of the Sample that was used in this Experiment. More details in the [Biosources and Samples](02-06-bio-sources.md) section.
  * *Technique* - Techniqu.e used by this Experiment. For example: ChipSeq or DNaseSeq. More details in the [Technique](02-08-techniques.md) section
  * *Project* - Project which this Experiment is associated. For example: ENCODE or Blueprint. More details in the [Project](02-09-projects.md) section.
  * *Description* - Description of the Experiment.
  * *Extra metadata* - Additional metadata. A key-value dictionary with extra information about the Experiment
  * *User* - User who inserted the Experiment.

The command [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments) is used to obtain all Experiments that match the given metadata content.
This command has the parameters: Genome Assembly, Epigenetic Mark, Sample Id, Technique, Project, and *user_key*.
All parameters, with the exception the *user_key*, are optional. Setting a parameter to *None* means that this parameter will not be used for the  Experiment selection. DFor example, it is possible to list all Experiments from the genome assembly hg19, by entering the genome assembly and passing an empty string to all others metadata parameters:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

all_experiments = server.list_experiments("hg19", "", "", "", "", user_key)
```

If we with to list all Experiments from the human genome assembly *hg19* with the epigenetic mark *H3K27me3* from the *ENCODE* project:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

h3k27me3_encode = server.list_experiments("hg19", "h3k27me3", None, None, "ENCODE", user_key)
```
