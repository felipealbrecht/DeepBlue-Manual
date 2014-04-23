## Annotations

The **Annotations** have only the genome and user attributes. They are used for storing regions that does not belongs to a specific epigenetic mark, but to auxiliary data, for instance: CpG Islands and Genes. It is possible to list all available annotations using the [list_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-list_annotations) command. The *list_annotations* has only the *genome* and *user key* parameters. 

The following code exhibits how to retrieve a list of all annotations available for the genome assembly *hg19*:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

h3k27me3_encode = server.list_annotations("hg19", user_key)
``` 