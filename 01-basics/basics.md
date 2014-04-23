# DeepBlue Epigenomics Data Server

## Concept
DeepBlue is a data server that contains epigenomic data from main Epigenomic Project: [ENCODE](https://www.genome.gov/encode/), [Roadmap Epigenomic Project](http://www.roadmapepigenomics.org/) (soon), and [BLUEPRINT](Blueprint). 

## This manual
This manual cover the entire DeepBlue usage: [Creating an user](creating-user.md), [Searching for data](searching.md), Inserting new data, Selecting data, Operating the data, and Retrieving data. The coding examples are written in *Python 2.7* but they can be easily adapted to others programming language.

## Access
All access are made to our XML-RPC server located at [http://deepblue.mpi-inf.mpg.de/xmlrpc](http://deepblue.mpi-inf.mpg.de/xmlrpc).

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"
server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)
```

## Reference Guide
A list of all commands is available at [DeepBlue API Page](http://deepblue.mpi-inf.mpg.de/api.html). This list is updated automatically when new commands are inserted or modified.