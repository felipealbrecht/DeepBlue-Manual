## Inserting Annotation

The [add_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-add_annotation) requires only the ```name```, ```genome```, ```description```, ```data```, ```format```, and ```extra_metadata```. All these parameters have the same meaning of their respective parameters in the  [add_experiment](http://deepblue.mpi-inf.mpg.de/api.html#api-add_experiment). The ```format```is the only exception, because [add_annotations](http://deepblue.mpi-inf.mpg.de/api.html#api-add_annotation) *only accepts data in the BED format, not accepting in WIG format*.

 