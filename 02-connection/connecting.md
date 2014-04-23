# Connecting

DeepBlue uses XML-RPC Protocol for communication. XML-RPC because is a simple protocol, having implementation in almost all programming languages. Even that this manual focus on *Python 2.7*, DeepBlue commands must work on all programming languages. 

To use DeepBlue, you must have an User Key.


```python
import xmlrpclib
user_key = "fillhere"

url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

print server.echo(user_key)
```

The server should return:

```python
['okay', 'Deep Blue (0.8.4) says hi to Your Name']
```