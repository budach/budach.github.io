# Class One_Hot_Encoder - Documentation

The One_Hot_Encoder class provides functions to encode a string over a given alphabet into an integer matrix of shape (len(string), len(alphabet)) where each row represents a position in the string and each column represents a character from the alphabet. Each row has exactly one 1 at the matching alphabet character and consists of 0s otherwise.

## Methods - Overview

| name | description |
|:-|:-|
| \_\_init\_\_ | Initialize the object with an alphabet. |
| encode | Encode a sequence into a one-hot integer matrix. |
| decode | Decode a one-hot integer matrix into the original sequence. |
## \_\_init\_\_

``` python
def __init__(self, alphabet)
```
Initialize the object with an alphabet. 

| parameter | type | description |
|:-|:-|:-|
| alphabet | str | The alphabet that will be used for encoding/decoding (e.g. "ACGT"). |
## encode

``` python
def encode(self, sequence)
```
Encode a sequence into a one-hot integer matrix.  The sequence should only contain characters from the alphabet provided to \_\_init\_\_. 

| parameter | type | description |
|:-|:-|:-|
| sequence | str | The sequence that should be encoded. |

| returns | type | description |
|:-|:-|:-|
| one_hot | numpy.ndarray | A numpy array with shape (len(sequence), len(alphabet)). |
## decode

``` python
def decode(self, one_hot)
```
Decode a one-hot integer matrix into the original sequence. 

| parameter | type | description |
|:-|:-|:-|
| one_hot | numpy.ndarray | A one-hot matrix (e.g. as created by the encode function). |

| returns | type | description |
|:-|:-|:-|
| sequence | str | The sequence that is represented by the one-hot matrix. |
