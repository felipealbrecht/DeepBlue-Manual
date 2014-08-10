## Accessing DeepBlue
All access to DeepBlue is made thought the XML-RPC protocol to the server located at [http://deepblue.mpi-inf.mpg.de/xmlrpc](http://deepblue.mpi-inf.mpg.de/xmlrpc).

Note that while the examples in this manual focus on *Python 2.7* programming language, DeepBlue commands must work on nearly all programming languages. For XML-RPC-based  access to DeepBlue from other languages, please check the following resources:
 * Java - [Apache XML-RPC](http://ws.apache.org/xmlrpc/)
 * R (bioconductor)- [XMLRPC](http://bioconductor.org/packages/devel/extra/html/XMLRPC.html)
 * PHP - [XML-RPC](http://php.net/manual/en/book.xmlrpc.php)
 * Others programming languages [google it](https://www.google.com/search?q=xml+rpc+%3Cyour%20programming%20language%3E)

We use the library [xmlrpclib](https://docs.python.org/2/library/xmlrpclib.html) for accessing the DeepBlue Server in the *Python 2.7*. In *Python 3*, the library [xmlrpc.client](https://docs.python.org/3.0/library/xmlrpc.client.html) must be used.
For accessing DeepBlue, firstly, we must define a object.
As example, the following snippet instantiate a object, called *server*, that will be used for accessing the DeepBlue server. This snippet should be used as a prefix for all future examples.

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"
server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)
```

The *user_key* stores your credentials for accessing the server. The section [Creating User](04-creating-user.md) describes how to obtain your *user_key*.
In the final line of the example above, we create an object for accessing the server. Be sure to use UTF-8 as encoding, and *allow_none=True*.

Execute the following code:
```python
import xmlrpclib
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"
server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)
server.echo(None)
```

The previous code should print: ```['okay', 'Deep Blue (0.9.5) says hi to a Stranger']```

Some commands, for example [list_experiments](http://deepblue.mpi-inf.mpg.de/api.html#api-list_experiments), have some parameters that are optional. For that, it is possible to inform *None* (or the *null* value in your favorite programming language) or an empty string (```""```).
The last line of the previous snipped can be rewritten as:
```python
server.echo("")
```

### Commands Response

The commands response are a tuple with two elements. The first elements is the status: returning ```okay``` when the command was successfully executed or ```error``` when a error occurred.
When the command were executed successfully (```okay```), the second tuple element is the command result, otherwise, this element contains a error message.

A good practice is to check the result status after each the command execution:

```python
(status, result) = server.echo(None)
if status == "error":
  print "Error : " + result
else:
  print result
```
