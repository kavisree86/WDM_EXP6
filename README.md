### EX6 Information Retrieval Using Vector Space Model in Python
### DATE: 
### AIM: To implement Information Retrieval Using Vector Space Model in Python.
### Description: 
<div align = "justify">
Implementing Information Retrieval using the Vector Space Model in Python involves several steps, including preprocessing text data, constructing a term-document matrix, 
calculating TF-IDF scores, and performing similarity calculations between queries and documents. Below is a basic example using Python and libraries like nltk and 
sklearn to demonstrate Information Retrieval using the Vector Space Model.

### Procedure:
1. Define sample documents.
2. Preprocess text data by tokenizing, removing stopwords, and punctuation.
3. Construct a TF-IDF matrix using TfidfVectorizer from sklearn.
4. Define a search function that calculates cosine similarity between a query and documents based on the TF-IDF matrix.
5. Execute a sample query and display the search results along with similarity scores.

### Program:

import numpy as np
import pandas as pd

class BooleanRetrieval:
    def __init__(self):
        self.index = {}
        self.documents_matrix = None

    def index_document(self, doc_id, text):
        terms = text.lower().split()
        print("Document -", doc_id, terms)

        for term in terms:
            if term not in self.index:
                self.index[term] = set()
            self.index[term].add(doc_id)

    def create_documents_matrix(self, documents):
        terms = list(self.index.keys())
        num_docs = len(documents)
        num_terms = len(terms)

        self.documents_matrix = np.zeros((num_docs, num_terms), dtype=int)

        for i, (doc_id, text) in enumerate(documents.items()):
            doc_terms = text.lower().split()
            for term in doc_terms:
                if term in self.index:
                    term_id = terms.index(term)
                    self.documents_matrix[i, term_id] = 1

    def print_documents_matrix_table(self):
        df = pd.DataFrame(self.documents_matrix, columns=self.index.keys())
        print(df)

    def print_all_terms(self):
        print("All terms in the documents:")
        print(list(self.index.keys()))

    def boolean_search(self, query):
        query_terms = query.lower().split()
        results = None

        for term in query_terms:
            doc_ids = self.index.get(term, set())
            if results is None:
                results = doc_ids.copy()
            else:
                if term.startswith('not'):
                    results.difference_update(doc_ids)
                elif term == 'or':
                    results.update(doc_ids)
                elif term == 'and':
                    results.intersection_update(doc_ids)

        return list(results) if results else []

if __name__ == "__main__":
    indexer = BooleanRetrieval()

   
    documents = {
        1: "Python is a programming language",
        2: "Information retrieval deals with finding information",
        3: "Boolean models are used in information retrieval"
    }

    for doc_id, text in documents.items():
        indexer.index_document(doc_id, text)

    
    indexer.create_documents_matrix(documents)
    indexer.print_documents_matrix_table()


    indexer.print_all_terms()


    query1 = input("Enter your boolean query: ")
    results = indexer.boolean_search(query1)
    if results:
        print(f"Results for '{query1}': {results}")
    else:
        print("No results found for the query.")

### Output:
![Screenshot 2024-09-21 141156](https://github.com/user-attachments/assets/b2419000-3b34-4fcc-9039-947a9fa5a0f5)

### Result:
Thus, the implementation of Information Retrieval using Boolean model had been successfully done using
python

