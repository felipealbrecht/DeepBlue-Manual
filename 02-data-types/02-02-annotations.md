## Annotations

The **Annotations** data type only has the *genome* and *user* attributes. 
They are used for storing regions that do not belongs to a specific epigenomic experiment, but to general annotation data.
Examples of annotations are: CpG Islands and Genes. It is possible to list all available annotations using the [list_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-list_annotations) command. The *list_annotations* command has the parameters *genome* and *user key*.

The following code shows how to retrieve a list of all annotations available for the genome assembly *hg19*:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

hg19_annotations = server.list_annotations("hg19", user_key)
``` 
