## Creating user
To use DeepBlue is necessary to have an account. For that, send an email to [albrecht@mpi-inf.mpg.de](mailto:albrecht@mpi-inf.mpg.de), informing your name and affiliation. After processing, you will receive an email with an *user key*. Please, keep calm because it is a manual process.
The *user key* is your DeepBlue identification. It is **secret** and **must not be shared**, even with co-workers. If you have any problem with your key: missing, please, contact us.

The [echo](http://deepblue.mpi-inf.mpg.de/api.html#api-echo) command can be used to verify the *user key*. 
The following code is an example of how can you test your *user key*. 
Remember to change ```user_key = "userkey123"``` to your proper user key. 

```python
import xmlrpclib
user_key = "userkey123"

url = "http://deepblue.mpi-inf.mpg.de/xmlrpc"

server = xmlrpclib.Server(url, encoding='UTF-8', allow_none=True)

print server.echo(user_key)
```

The ```echo``` command should return: ```['okay', 'Deep Blue (0.8.4) says hi to Your Name']```. If it returned ```['okay', 'Deep Blue (0.8.4) says hi to a Stranger']```, please, check again your user key or contact us.
