# File utils_io.py - Documentation

## Methods - Overview

| name | description |
|:-|:-|
| save\_model | Save a placeholder.Model object. |
| load\_model | Load a placeholder.Model object. |
| save\_data | Save a placeholder.Data object. |
| load\_data | Load a placeholder.Data object. |
## save\_model

``` python
def save_model(model, file_path)
```
Save a placeholder.Model object. 

 This function creates two files: a pickled version of the placeholder.Model object and an hdf5 file of the actual keras model (e.g. if file\_path is 'model' two files are created: 'model' and 'model.h5') 



| parameter | type | description |
|:-|:-|:-|
| model | placeholder.Model | A Model object. |
| file_path | str | A file name. |
## load\_model

``` python
def load_model(file_path)
```
Load a placeholder.Model object. 



| parameter | type | description |
|:-|:-|:-|
| file_path | str | An existing file (the file file_path.h5 must also exist, see save_model()). |

| returns | type | description |
|:-|:-|:-|
| model | placeholder.Model | A Model object. |
## save\_data

``` python
def save_data(data, file_path)
```
Save a placeholder.Data object. 

 The object will be pickled to disk. 



| parameter | type | description |
|:-|:-|:-|
| file_path | str | A file name. |
## load\_data

``` python
def load_data(file_path)
```
Load a placeholder.Data object. 



| parameter | type | description |
|:-|:-|:-|
| file_path | str | A file containing a pickled placeholder.Data object. |

| returns | type | description |
|:-|:-|:-|
| data | placeholder.Data | The Data object loaded from file. |
