## User keys
The *user_key* is your unique and personal identification for the DeepBlue Epigenomic Data Server.

It is **secret** and **must not be shared**, even with co-workers. Contact us if you encounter any problems with your key.

The easiest way to verify your *user_key* is through the [echo](http://deepblue.mpi-inf.mpg.de/api.html#api-echo) command.
The following code shows how you can verify your *user_key*.
Before executing this code, change the variable ```user_key``` to your proper *user_key*.

```python
import xmlrpclib
user_key = "userkey123"
url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"
server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)
print server.echo(user_key)
```

The ```echo``` command should return: ```['okay', 'Deep Blue (0.9.5) says hi to Your Name']```.
Please verify your *user_key* if the command returned ```['okay', 'Deep Blue (0.9.5) says hi to a Stranger']```.