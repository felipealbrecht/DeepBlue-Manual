## User keys
The *user key* is your DeepBlue identification. It is **secret** and **must not be shared**, even with co-workers. Contact us if you encounter any problems with your key.

The [echo](http://deepblue.mpi-inf.mpg.de/api.html#api-echo) command can be used to verify the *user key*. 
The following code shows how can you verify your *user key*.
Be sure to change ```user_key = "userkey123"``` to your proper user key. 

```python
import xmlrpclib
user_key = "userkey123"

url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

print server.echo(user_key)
```

The ```echo``` command should return: ```['okay', 'Deep Blue (0.8.4) says hi to Your Name']```. If it returned ```['okay', 'Deep Blue (0.8.4) says hi to a Stranger']```, please, verify your user key.
