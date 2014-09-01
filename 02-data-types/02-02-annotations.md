## Annotations

The auxiliary genomic regions data is organized as Annotations in DeepBlue.
Each Annotation is composed by a regions set, a name, *Genome*, and *user* attributes.

Annotations are used to store genomic regions that do not come from an epigenomic Experiment, but contain other (epi-)genetic information. Examples of Annotations are: CpG Islands and Genes. It is possible to list all available Annotations using the [list_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-list_annotations) command. The *list_annotations* command has two parameters: *Genome* and *user_key*.

The following snipped demonstrate how to list all available Annotations for the genome assembly *hg19*:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

hg19_annotations = server.list_annotations("hg19", user_key)
```
