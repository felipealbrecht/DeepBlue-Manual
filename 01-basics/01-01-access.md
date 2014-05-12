## Access
All access to DeepBlue is made thought the XML-RPC protocol to the server located at [http://deepblue.mpi-inf.mpg.de/xmlrpc](http://deepblue.mpi-inf.mpg.de/xmlrpc). 

Even that this manual focus on *Python 2.7*, DeepBlue commands must work on all programming languages. For access DeepBlue from other languages, please check:
 * Java - [Apache XML-RPC](http://ws.apache.org/xmlrpc/)
 * R (bioconductor)- [XMLRPC](http://bioconductor.org/packages/devel/extra/html/XMLRPC.html)
 * PHP - [XML-RPC](http://php.net/manual/en/book.xmlrpc.php)
 * Others programming languages [google it](https://www.google.com/search?q=xml+rpc+%3Cyour%20programming%20language%3E)

The following snippet should be used in all examples: 

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"
server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)
```

We use [xmlrpclib](https://docs.python.org/2/library/xmlrpclib.html) for accessing the XML-RPC server.
The *user_key* is your credential for access the server. The section [Creating User](04-creating-user.md) describes how to obtain your *user_key*.
In the end, we create an instance of the server. Take care to use UTF-8 as encoding, and *allow_none=True*.

Execute the following code:
```python 
import xmlrpclib
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"
server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)
server.echo(None)
```

It should print: ```['okay', 'Deep Blue (0.9.0) says hi to a Stranger']```

Every DeepBlue command return a tuple with two elements: the result status and the result content.
The result status can be ```"okay"``` or ```"error"```. 
The result content is the data returned by the operation, the exception is when the result status is ```"error"```, so the result content will be a message informing the error reason.

A good practice is to check the result status after each the command execution:

```python
(status, result) = server.echo(None)
if status == "error":
  print "Error : " + result
else:
  print result
```