Assignement 1 - CSI4107

Students:
Yassin, Chad : 300240007
Khelifa, Anas : 
Fuad, Pronoy : 300269503

 ########################### 1 - Division of Tasks:  ###########################
Chad
- Step 2 : Indexing ( block 2 in info_retrieval.ipynb)

Anas
- Step 3 : Retrieval and Ranking ( block 3 in info_retrieval.ipynb)

Pronoy 
- Step 1 : Preprocessing ( block 1 in info_retrieval.ipynb)


 ########################### 2 - Detailed note about the functionality of our programs ###########################
Step 1 works by : Pronoy write here...

Step 2 works by :
 -1 Taking the preprocessed corpus developped in step 1. 
 -2 Using a defaultdict to act as the inverted index ensuring that each word will be mapped to IDs without having duplicates. 
 -3 Iterating over the items in the corpus to extract the ID and the token. 
 -4 Then iterating over every token, appending IDs that pertain to that token (example the word alter has the IDs '10071552', '10190462', '10314816'.. and so on because it appears in those documents.
 -5 Once this process is done the elements in the inverted index are iterated over: the item is printed to the console example: matter: ['11880289', '13322804', '13770184'... and in the same iteration, the word and it's IDs are being appended to a list that's elements are formatted like a json file.
 -6 Finnaly the json library is used to create inverted_index.json which contains the inverted index.

Step 3 works by : Anas write here...

 ########################### 3 - complete instructions on how to run ###########################

To run the program: 
 -1 clone this repositiory to your computer
 -2 You can chose to create your own corpus or use the current one, please use the same format as corpus.jsonl
 -3 Ensure that you computer has python and the following libraries installed: (use pip to install missing dependencies)
 -4 Run block #1 Preprocessing : You will have the file preprocessed_corpus.xlsx saved to the root directory, containing the corpus.
 -5 Run block #2 Inverted indexing : You will have the file inverted_index.json saved to the root direcory, containing the revers index.
 -6 Run block #3 ...Anas write here...

 ########################### 4 - explanation ###########################

Step 1 : Pronoy write here...

Step 2 :
 -1 defaultdict from the collections package is used as a means to hold the reverse index, this is done as a defaultdict automatically handles missing keys. defaultdict generates a default value for a key that is trying to be accessed that is yet to exist.
 -2 the list json_data is a simpele python list that contains dictionaries which have 2 keys, "word" that contains the words and "ids" which is a string that contains all the ids associated to the word.

Step 3  : Anas write here...

########################### 5 - Mean Average Precision (MAP) score ###########################
Anas write here...
