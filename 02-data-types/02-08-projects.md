## Projects

The projects controlled vocabulary contains the projects responsible for generating the epigenomics data.
DeepBlue contains the ENCODE and Blueprint Epigentics projects inserted.
We will automatically create the DEEP and Roadmap projects when we import their data.

It is possible to list all projects with the [list_projects](http://deepblue.mpi-inf.mpg.de/api.html#api-list_projects) command:
```python
server.list_projects(user_key)
```

```python
['okay', [['p1', 'ENCODE'], ['p2', 'Blueprint Epigenetics']]]
```

Similar projects names can be found using [list_similar_projects](http://deepblue.mpi-inf.mpg.de/api.html#api-list_similar_projects)

The command [add_project](http://deepblue.mpi-inf.mpg.de/api.html#api-add_project) is used to insert a project.
Not every user has permission to insert new projects.