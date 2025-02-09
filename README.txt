Assignement 1 - CSI4107

Students:
Yassin, Chad : 300240007
Khelifa, Anas : 300257055
Fuad, Pronoy : 300269503

 ########################### 1 - Division of Tasks:  ###########################
Chad
- Step 2 : Indexing ( block 2 in info_retrieval.ipynb)

Anas
- Step 3 : Retrieval and Ranking ( block 3 in info_retrieval.ipynb)

Pronoy 
- Step 1 : Preprocessing ( block 1 in info_retrieval.ipynb)


 ########################### 2 - Detailed note about the functionality of our programs ###########################
Step 1 works by : 
 Input: Each document is read from corpus.jsonl. Our documents contain the keys _id (document identifier) and text (the full content).
  Processing:
  -1 Tokenization: The word_tokenize function splits the text into individual tokens.
  -2 Filtering: A regular expression is used to remove non-alphanumeric characters, and all tokens are converted to lowercase.
  -3 Stopword Removal: Common English stopwords (e.g., "the", "and", etc.) are removed using NLTK’s stopword list.
  -4 Stemming: The Porter Stemmer is applied to reduce words to their root forms (e.g., "running" becomes "run").
 Output: The processed tokens for each document are stored in a Python dictionary (the corpus), and a sample of the output is exported to an Excel file (preprocessed_corpus.xlsx) for verification

Step 2 works by :
 -1 Taking the preprocessed corpus developped in step 1. 
 -2 Using a defaultdict to act as the inverted index ensuring that each word will be mapped to IDs without having duplicates. 
 -3 Iterating over the items in the corpus to extract the ID and the token. 
 -4 Then iterating over every token, appending IDs that pertain to that token (example the word alter has the IDs '10071552', '10190462', '10314816'.. and so on because it appears in those documents.
 -5 Once this process is done the elements in the inverted index are iterated over: the item is printed to the console example: matter: ['11880289', '13322804', '13770184'... and in the same iteration, the word and it's IDs are being appended to a list that's elements are formatted like a json file.
 -6 Finnaly the json library is used to create inverted_index.json which contains the inverted index.

Step 3 works by :

-1 The program reads the inverted index (inverted_index.json), which maps words to document IDs. It loads the preprocessed corpus (preprocessed_corpus.xlsx), ensuring each document ID is mapped to its tokenized content. It retrieves test queries from queries.jsonl and test.tsv for evaluation.
-2 Queries are lowercasd and tokenized to match the format of the preprocessed corpus. If necessary, stemming and stopword removal are applied to ensure consistency with the corpus.
-3 For each query, the system extracts terms and searches for them in the inverted index. A set of document IDs is created containing at least one of the query words.
-4 The system uses TF-IDF vectorization to represent queries and documents numerically. Cosine similarity is computed between the query and each relevant document. The documents are sorted in descending order based on their similarity scores.
-5 The ranked list for each query is written to ranked_results.txt, formatted as: query_id Q0 doc_id rank score run_name. This file contains the top 100 most relevant documents per query.
-6 The system uses the test queries (test.tsv) to evaluate retrieval performance. The top-ranked results are saved in Results, following the required format for submission.
At the end of Step 3, two key output files are generated:
ranked_results.txt → Retrieval results based on cosine similarity ranking.
Results → Evaluation output formatted for submission.


 ########################### 3 - complete instructions on how to run ###########################

To run the program: 
 -1 clone this repositiory to your computer
 -2 You can chose to create your own corpus or use the current one, please use the same format as corpus.jsonl
 -3 Ensure that you computer has python and the following libraries installed: (use pip to install missing dependencies)
 -4 Run block #1 Preprocessing : You will have the file preprocessed_corpus.xlsx saved to the scifact directory, containing the corpus.
 -5 Run block #2 Inverted indexing : You will have the file inverted_index.json saved to the scifact direcory, containing the revers index.
 -6 Run block #3 Retrieval and Ranking: You will have the files ranked_results.txt and Results saved to the scifact directory, containing the results based on cosine similarity ranking and the test results.

 ########################### 4 - explanation ###########################

Step 1 : 
I used Python and NLTK to tokenize the text, filter out unwanted characters and numbers, remove stopwords, and perform stemming. The function preprocess(text) encapsulates these steps.

1- Tokenization is done via word_tokenize().
2- Filtering and Lowercasing: Using regular expressions to remove punctuation and ensure consistency.
3- Stopword Removal ensures that common words do not clutter the index.
4- Stemming reduces the tokens to their base forms, improving matching across different forms of a word.

Step 2 :
 -1 defaultdict from the collections package is used as a means to hold the reverse index, this is done as a defaultdict automatically handles missing keys. defaultdict generates a default value for a key that is trying to be accessed that is yet to exist.
 -2 the list json_data is a simpele python list that contains dictionaries which have 2 keys, "word" that contains the words and "ids" which is a string that contains all the ids associated to the word.

Step 3  :
I implemented retrieval and ranking using the Vector Space Model with cosine similarity to rank documents based on their relevance to queries.
-1 Data loading: The inverted index (inverted_index.json), preprocessed corpus (preprocessed_corpus.xlsx), and queries (queries.jsonl, test.tsv) are loaded.
-2 Query processing: Queries are lowercased and tokenized to match the format of the preprocessed corpus.
-3 Document retrieval: The inverted index is used to find documents containing at least one query word, reducing the search space.
-4 Cosine similarity Computation: Documents are converted to TF-IDF vectors, and cosine similarity is used to rank them based on query relevance.
-5 Saving ranked Results: The top 100 documents for each query are written to ranked_results.txt.
-6 Test query evaluation: The system runs on test queries from test.tsv, saving ranked results in Results for submission.


########################### 5 - Mean Average Precision (MAP) score ###########################
Titles + full text Mean Average Precision (MAP): 0.3491 - Calculated using Results and qrels.txt file
qrels.txt is test.tsv file converted in qrels format.