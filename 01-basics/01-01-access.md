## Access
All access to DeepBlue is made thought the XML-RPC protocol to the server located at [http://deepblue.mpi-inf.mpg.de/xmlrpc](http://deepblue.mpi-inf.mpg.de/xmlrpc). 

Note that the example from this manual focus on *Python 2.7*, but DeepBlue commands work on nearly all programming languages. For access DeepBlue from other languages, please check the following resources:
 * Java - [Apache XML-RPC](http://ws.apache.org/xmlrpc/)
 * R (bioconductor)- [XMLRPC](http://bioconductor.org/packages/devel/extra/html/XMLRPC.html)
 * PHP - [XML-RPC](http://php.net/manual/en/book.xmlrpc.php)
 * Others programming languages [google it](https://www.google.com/search?q=xml+rpc+%3Cyour%20programming%20language%3E)

The following snippet should be used as a prefix in all examples:

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"
server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)
```

We use [xmlrpclib](https://docs.python.org/2/library/xmlrpclib.html) for accessing the XML-RPC server.
The *user_key* are your credentials for access the server. The section [Creating User](04-creating-user.md) describes how to obtain your *user_key*.
In the end, we create an object for accessing the server. Be sure to use UTF-8 as encoding, and *allow_none=True*.

Execute the following code:
```python 
import xmlrpclib
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"
server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)
server.echo(None)
```

It should print: ```['okay', 'Deep Blue (0.9.0) says hi to a Stranger']```

Every DeepBlue command returns a tuple with two elements: the result status and the result content.
The result status can be ```"okay"``` or ```"error"```. 
The result content is the data returned by the operation, the exception is when the result status is ```"error"```, so the result content will be an error message.

A good practice is to check the result status after each the command execution:

```python
(status, result) = server.echo(None)
if status == "error":
  print "Error : " + result
else:
  print result
```