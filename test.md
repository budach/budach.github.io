# Class Data - Documentation

The Data class provides a convenient way to handle DNA and RNA sequence and structure data for different classes. Sequence and structure data are automatically converted into one-hot encoded matrices and split into training/validation/test sets. The data object can then be passed to Grid_Search or Model objects for easy training and evaluation.

## Methods - Overview

| name | description |
|:-|:-|
| \_\_init\_\_ | Initialize the object by providing sequence files and an alphabet. |
| train\_val\_test\_split | bla |
## \_\_init\_\_

``` python
def __init__(self, class_files, alphabet)
```
Initialize the object by providing sequence files and an alphabet. 

 If the goal is to do single-label classification a list of fasta files must be provided (one file per class, the first file will correspond to 'class\_0' etc.). In this case fasta headers are ignored. If the goal is multi-label classification a single fasta file must be provided and headers must indicate class membership as a comma-separated list (e.g. header '\>0,2' means that the sequence belongs to class 0 and 2). 

 For sequence-only files fasta entries have no format restrictions. For sequence-structure files each sequence and structure must span a single line, e.g.: 

  \>0,2  
  CCCCAUAGGGG  
  ((((...)))) (-3.3)  
  SSSSHHHSSSS  
 

 This kind of format is the default output of RNAfold. The third line containing the annotated structure string can be omitted if you want to do the training on the dot-bracket strings. 

 Important: All sequences in all files must have the same length. 

 The provided alphabet must match the content of the fasta files. For sequence-only files a single string ('ACGT' or 'ACGU') should be provided, for sequence-structure files a tuple (('ACGU', 'HIMS') to use the annotated structures or ('ACGU', '().') to use dot-bracket structures). 



| parameter | type | description |
|:-|:-|:-|
| class_files | str or [str] | A fasta file (multi-label) or a list of fasta files (single-label). |
| alphabet | str or tuple(str,str) | A string for sequence-only files and a tuple for sequence-structure files. |
## train\_val\_test\_split

``` python
def train_val_test_split(self, portion_train, portion_val, seed = None)
```
bla 

 bla 



| parameter | type | description |
|:-|:-|:-|
| portion_train | float | bla |
| portion_val | float | bla |
| seed | int | bla |
