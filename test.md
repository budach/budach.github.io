# File utils_misc.py - Documentation

## Methods - Overview

| name | description |
|:-|:-|
| annotate\_structures | Annote secondary structure predictions with structural contexts. |
| predict\_structures | Predict secondary structures for RNA sequences. |
| get\_performance\_report | Get a performance overview of a classifier. |
| save\_as\_meme | Save sequence (or structure) motifs in MEME format. |
| run\_tomtom | Compare a MEME file against a database using TomTom. |
## annotate\_structures

``` python
def annotate_structures(input_file, output_file)
```
Annote secondary structure predictions with structural contexts. 

 Given dot-bracket strings this function will annote every character as either 'H' (hairpin), 'S' (stem), 'I' (internal loop) or 'M' (multi loop). The input file must be a fasta formatted file and each sequence and structure must span a single line: 

  \>header  
  CCCCAUAGGGG  
  ((((...)))) (-3.3)  
 

 This is the default format of RNAfold. The output file will then contain the annotated string as a third line: 

  \>header  
  CCCCAUAGGGG  
  ((((...)))) (-3.3)  
  SSSSHHHSSSS  
 



| parameter | type | description |
|:-|:-|:-|
| input_file | str | A fasta file containing secondary structure predictions. |
| output_file | str | A fasta file with additional structure annotations. |
## predict\_structures

``` python
def predict_structures(input_file, output_file, num_processes = 1, annotate = False)
```
Predict secondary structures for RNA sequences. 

 This is a convenience function to get quick RNA secondary structure predictions. The function will try to use the RNAlib python bindings or the RNAfold binary to perform predictions. If neither can be found the function returns without creating an output file. Using the RNAlib python bindings is preferred as it is much faster. 

 Entries of the output file look as follows: 

  \>header  
  CCCCAUAGGGG  
  ((((...)))) (-3.3)  
  SSSSHHHSSSS  
 

 The third line will only exist if annotate = True. 

 Warning: Due to the way Python works spinning up additional processes means copying the complete memory of the original process, i.e. if the original processes already uses 5 GB of RAM each additional process will use 5 GB as well. 



| parameter | type | description |
|:-|:-|:-|
| input_file | str | A fasta file with RNA sequences. |
| output_file | str | A fasta file with sequences and structures. |
| num_processes | int | The number of parallel processes to use for prediction. (default: 1) |
| annotate | bool | Also output the annotated structure string in addition to the dot-bracket string. (default: false) |
## get\_performance\_report

``` python
def get_performance_report(labels, predictions)
```
Get a performance overview of a classifier. 

 The report contains precision, recall, f1-score, ROC-AUC and Precision-Recall-AUC for every class (in a 1 vs. rest approach) and weighted averages (weighted by the the number of sequences 'n' in each class). 



| parameter | type | description |
|:-|:-|:-|
| labels | numpy.ndarray | A binary matrix of shape (num sequences, num classes) containing the true labels. |
| predictions | numpy.ndarray | A matrix of shape (num sequences, num classes) containing predicted probabilites. |

| returns | type | description |
|:-|:-|:-|
| report | str | Summary table of the above mentioned performance measurements. |
## save\_as\_meme

``` python
def save_as_meme(logos, file_path)
```
Save sequence (or structure) motifs in MEME format. 



| parameter | type | description |
|:-|:-|:-|
| logos | [placeholder.Motif] | A list of Motif objects. |
| file_path | str | The name of the output text file. |
## run\_tomtom

``` python
def run_tomtom(motif_file, output_folder, database, options = None)
```
Compare a MEME file against a database using TomTom. 

 Default options string: "-min-overlap 5 -verbosity 1 -xalph -evalue -thresh 0.1" 



| parameter | type | description |
|:-|:-|:-|
| motif_file | str | A MEME file. |
| output_folder | str | The folder the TomTom output will be saved in. |
| database | str | A MEME file serving as the database to compare against. |
| option | str | Command line options passed to TomTom. |
