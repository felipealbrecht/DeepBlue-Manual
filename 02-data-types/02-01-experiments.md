## Experiments

The Epigenomic data is organized as Experiments into DeepBlue.
Each experiment is compound by a regions set and an associated metadata.

One Experiments has the following metadata information:
  * *Name* - Experiment name - Should be unique
  * *Genome* - genome assembly used by this experiment. More details in the [genomes](02-04-genomes.md) section
  * *Epigenetic mark* - Epigenetic mark of the experiment. For example: methylation or some Histone Modification. More details in the [epigenetic marks](02-05-epigenetic-marks.md) section
  * *Sample* - Identification of the sample that was used in this Experiment. More details in the [bio sources and samples](02-06-bio-sources.md) section
  * *Technique* - Technique used by this experiment. For example: ChipSeq or DNaseSeq. More details in the [technique](02-08-techniques.md) section
  * *Project* - Project that this experiment is associated. For example: ENCODE or Blueprint. More details in the [project](02-09-projects.md) section
  * *Description* - Description of the experiment
  * *Extra metadata* - Additional metadata. A key-value dictionary with extra information about the experiment
  * *User* - User that inserted the experiment.

The command [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments) is used to obtain all experiments that match the given metadata content.
This command has the genome assembly, epigenetic mark, sample id, technique, project, and the *user key* as parameters.
All parameters, with exception *user key*, are optional. Setting a parameter to *None* means that this parameter will not be used for the  experiments selection. As an example, it is possible to list all experiments, from the genome assembly hg19, informing the genome assembly and using an empty string in all others metadata parameters:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

all_experiments = server.list_experiments("hg19", "", "", "", "", user_key)
```

If we want to list all experiments from the human genome assembly *hg19*, the epigenetic mark *H3K27me3* from the *ENCODE* project:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

h3k27me3_encode = server.list_experiments("hg19", "h3k27me3", None, None, "ENCODE", user_key)
```
