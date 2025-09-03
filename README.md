README
 1. Team Information
    -   Team Members: Pronoy Fuad, Chad Yassin, Anas Khelifa

Task Division
 Anas Khelifa : System Implementation and Initial Results
    1.	Responsibilities:
        -	Implement or update the initial classical IR system (from Assignment 1) to produce up to 100 documents per query.
        -	Apply the first advanced neural retrieval method (e.g., BERT, Universal Sentence Encoder, or sent2vec) for re-ranking the documents.
        -	Generate vectors for queries and documents using the selected neural model.
        -	Ensure the system generates results in the required format.
    2.	Deliverables:
        -	Results file with top 10 documents per query (intermediate output for the initial IR system and re-ranked results for one neural method).
        -	Explanation of how the neural model was integrated into the system.
 Chad Yassin : Advanced Neural Models and Evaluation
    1.	Responsibilities:
        -	Implement a second advanced neural retrieval method (e.g., doc2vec, GPT embeddings, or another model) for re-ranking documents.
        -	Optimize the second method for performance and accuracy (e.g., reduce computation time using boolean indexing or query filtering).
        -	Evaluate both advanced neural methods using MAP and P@10 metrics.
    2.	Deliverables:
        -	Results file for the second neural retrieval method.
        -	Performance evaluation of both methods (MAP and P@10 scores).
        -	Highlight the best-performing method and discuss results.
 Pronoy Fuad: Documentation and Submission
    1.	Responsibilities:
    -	Create the README file, ensuring it includes:
        -	Names, student numbers, and task divisions.
        -	Detailed description of the functionality of the implemented programs.
        -	Complete instructions on how to run the system.
        -	Explanation of algorithms, data structures, and optimizations.
        -	Discussion of the results, including the first 10 answers to Queries 1 and 3.
    -	Verify that the results file is in the correct format and includes results for all test queries.
    -	Ensure all programs run correctly and package the assignment into a zip file for submission.
    2.	Deliverables:
        -	Complete README file (PDF, plain text, or Word format).
        -	Finalized Results file with all test queries.
        -	Submission-ready zip file including all programs, README, and Results file.	

Evaluation

Two methods were evaluated for ranking query results:
    1.	TF-IDF combined with SBERT (all-MiniLM-L6-v2)
        -	Results:
            -   MAP: 0.5916
    2.	TF-IDF combined with SBERT (all-MiniLM-L12-v2)
        -	Results:
            -	MAP: 0.5585

MAP Evaluation
 The Mean Average Precision (MAP) evaluates the overall ranking quality. A higher MAP score indicates better alignment with the relevance judgments.
    -	The all-MiniLM-L6-v2 model achieved the highest MAP score of 0.5916 compared to the all-MiniLM-L12-v2 model's 0.5585.
    -	This indicates that the all-MiniLM-L6-v2 model was more effective in ranking documents relevant to the queries.


Program Functionality
    -	Main Script: Executes the retrieval and ranking tasks.
    -	Components:
        -	Inverted Index: How it maps words to document IDs.
        -	TF-IDF Retrieval: Selects the top 100 documents based on cosine similarity.
        -	Neural Re-Ranking: Uses SBERT to refine the top 100 documents.
        -	MAP Calculation: Computes Mean Average Precision to evaluate performance.

How to Run
 Step-by-step instructions:
    1.	Dependencies:
        -	Python 3.x
        -	Required libraries: pandas, numpy, scikit-learn, sentence-transformers, openpyxl
        -	Installation: pip install -r requirements.txt
    2.	Input Files:
        -	scifact/inverted_index.json
        -	scifact/preprocessed_corpus.xlsx
        -	scifact/queries.jsonl
        -	scifact/qrels.txt
    3.	Execution:
        -	Run main() in the script to generate results.
        -	Use compute_map() to evaluate the results.
        -	Command: python script_name.py

Algorithms Used
 1.	TF-IDF Retrieval:
    -	TF-IDF (Term Frequency-Inverse Document Frequency) was used to identify the most relevant documents for each query. It computes the importance of a term in a document relative to the entire corpus.
    -	Cosine similarity was applied to measure the similarity between the query vector and document vectors.
 2.	Neural Re-ranking:
    -	A Sentence-BERT (SBERT) model was used for neural re-ranking. SBERT computes dense embeddings for sentences and efficiently finds semantic similarity between the query and document texts.
    -	Cosine similarity between query and document embeddings was calculated for fine-grained ranking.

Data Structures
 1.	Inverted Index:
    -	Implemented as a dictionary where keys are words (terms) and values are lists of document IDs containing those words.
    -	Efficient for retrieving documents relevant to a query by looking up the terms in the index.
 2.	Corpus:
    -	Stored as a dictionary mapping document IDs to tokenized text representations of the document. This allows for quick retrieval of document content for scoring and ranking.
 3.	Query List:
    -	Maintained as a list of tuples containing query IDs and query text. This structure ensures the correct processing order.

Optimizations
 1.	Filtering Relevant Documents with Inverted Index:
    -	Instead of comparing the query with all documents in the corpus, the inverted index was used to filter out only those documents containing query terms.
    -	This significantly reduces the computational load by narrowing down the candidate documents.
 2.	Sparse and Dense Retrieval Pipeline:
    -	The pipeline combines the efficiency of sparse retrieval (TF-IDF) to pre-filter documents and the effectiveness of dense retrieval (SBERT) for re-ranking.
    -	TF-IDF selects the top 100 documents, which are then refined by SBERT, minimizing the computational cost of embedding and similarity computation.
 3.	Vectorization with Scikit-learn:
    -	TF-IDF vectorization and cosine similarity computations were optimized using the Scikit-learn library for fast and efficient linear algebra operations.
 4.	Neural Re-ranking with SBERT:
    -	Instead of encoding all documents in the corpus upfront, only the subset of documents retrieved by TF-IDF was processed. This reduces the memory footprint and speeds up the process.
 5.	Efficient Sorting:
    -	Scores were sorted using Python's in-built sort function, optimized for large datasets.

Sample Results
 ![alt text](image.png)

 The system ran a search for two different queries (Query 1 and Query 3). It retrieved and ranked documents based on their relevance to the queries. Here's an interpretation:

 Query 1 Results
    -	Top Document (Rank 1):
        Document with ID 4346436 has the highest relevance score of 0.4336 for Query 1. This means the system considers it the most relevant response to the query.
    -	Subsequent Ranks (Ranks 2–10):
        Documents are listed in descending order of relevance, with their scores gradually decreasing. For example, the document with ID 8610932 at Rank 10 has a score of 0.2199, indicating lower relevance compared to the top-ranked document.

 Query 3 Results
    -	Top Document (Rank 1):
        Document with ID 23389795 has the highest relevance score of 0.6056 for Query 3, making it the most relevant document retrieved for this query.
    -	Comparison Across Ranks:
        As with Query 1, documents are ranked by descending relevance scores. For example, the document with ID 18494847 at Rank 10 has a relevance score of 0.4177.

Discussion
 Performance Differences
    -	TF-IDF:
        -	Strong at retrieving documents explicitly matching query terms.
        -	Computationally efficient but limited in understanding semantics.
        -	Struggles with synonyms, context, and semantic relevance.
        -	Lower P@10 and MAP scores compared to neural methods.
    -   Neural Re-Ranking:
        -	Excels at semantic matching and contextual understanding using advanced models like BERT.
        -	Significantly improves top results’ relevance, reflected in higher evaluation scores.
        -	Computationally intensive and depends on pre-trained models’ quality.

 Key Challenges
    1.	High Computational Cost: Neural methods require substantial resources for embedding generation and re-ranking.
    2.	Query-Specific Results: Performance varied; simple queries sometimes saw marginal improvements over TF-IDF.
    3.	Handling Document Length: Some models struggled with very long documents due to token limits (e.g., 512 for BERT).

 Surprising Findings
    1.	Neural models retrieved contextually relevant documents even when query terms were absent, outperforming TF-IDF.
    2.	Precision at the top 10 results (P@10) showed notable improvement with neural methods.
    3.	Despite high accuracy, neural methods occasionally ranked tangentially related documents higher due to broad semantic matches.

 Conclusion
    -	Neural re-ranking methods outperformed TF-IDF, particularly for complex queries requiring semantic understanding.
    -	A hybrid approach combining TF-IDF for initial retrieval with neural re-ranking for refinement is ideal to balance efficiency and accuracy.


Results File
 Format the results as specified:
    QueryID Q0 DocID Rank Score Tag
    Save all results from the best system (neural re-ranking).