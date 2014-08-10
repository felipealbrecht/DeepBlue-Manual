## Annotations

The auxiliary genomic regions data is organized as Annotations in DeepBlue.
Each annotation is compound by a regions set, a name, *genome*, and *user* attributes.

Annotations are used to store genomic regions that does not come from an epigenomic experiment, but contains others (epi-)genetic information. Examples of annotations are: CpG Islands and Genes. It is possible to list all available annotations using the [list_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-list_annotations) command. The *list_annotations* command has two parameters: *genome* and *user key*.

The following snipped shows how to list of all annotations available for the genome assembly *hg19*:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

hg19_annotations = server.list_annotations("hg19", user_key)
```
