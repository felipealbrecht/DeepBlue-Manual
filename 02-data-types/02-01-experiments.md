## Experiments

All DeepBlue epigenomic data is organized into Experiments.  

An **Experiments** have the following attributes:
  * Name - experiment name
  * Genome - genome assembly used by this experiment. You can find more details in the **Genome** section
  * Epigenetic mark - Epigenetic mark of the experiment. You can find more details in the **Epigenetic mark** section
  * Sample - id of the sample, that is, a *bio_source* with more description on it. You can find more details in the **Sample** section
  * Technique - technique used by this experiment. You can find more details in the **Technique** section
  * Project - the project name. You can find more details in the **Project** section
  * Description - experiment description
  * extra_metadata - additional metadata. A key-value dictionary where the user can include extra information about the experiment.
  * user - identification of the user that inserted the experiment.

It is possible to obtain all experiments that match one or more attributes using the command [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments). 
This command receives the genome assembly name, epigenetic mark name, sample id, technique, project, and the *user key* as parameters.
All parameters, with exception *user key*, can be *None* (or the *null* value in your favorite programming language). 

For instance, it is possible to list all available experiments passing an empty string in all the parameters:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

all_experiments = server.list_experiments(None, None, None, None, None, user_key)
```

If we want to find all experiments from the human genome assembly *hg19*, the Epigenetic Mark *H3K27me3* from the *ENCODE* project:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

h3k27me3_encode = server.list_experiments("hg19", "h3k27me3", None, None, "ENCODE", user_key)
```