## Inserting Project

The [add_project](http://deepblue.mpi-inf.mpg.de/api.html#api-add_project) command requires the  ```name``` and ```description``` parameters.


```python
(status, p_id) = server.add_project("DEEP", "The German epigenome programme ‘DEEP’", user_key)
```
