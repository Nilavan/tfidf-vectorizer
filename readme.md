<h1 align="center">Custom implementation of tfidf vectorizer</h1>

## Intro to tfidf

Tf-idf stands for <em>term frequency-inverse document frequency</em>, and the tf-idf weight is a weight often used in information retrieval and text mining. This weight is a statistical measure used to evaluate how important a word is to a document in a collection or corpus. The importance increases proportionally to the number of times a word appears in the document but is offset by the frequency of the word in the corpus. Variations of the tf-idf weighting scheme are often used by search engines as a central tool in scoring and ranking a document's relevance given a user query.

One of the simplest ranking functions is computed by summing the tf-idf for each query term; many more sophisticated ranking functions are variants of this simple model.

Tf-idf can be successfully used for stop-words filtering in various subject fields including text summarization and classification.

## How to Compute

Typically, the tf-idf weight is composed by two terms: the first computes the normalized Term Frequency (TF), aka. the number of times a word appears in a document, divided by the total number of words in that document; the second term is the Inverse Document Frequency (IDF), computed as the logarithm of the number of the documents in the corpus divided by the number of documents where the specific term appears.

 <ul>
    <li>
<strong>TF:</strong> Term Frequency, which measures how frequently a term occurs in a document. Since every document is different in length, it is possible that a term would appear much more times in long documents than shorter ones. Thus, the term frequency is often divided by the document length (aka. the total number of terms in the document) as a way of normalization: <br><br>

<p align="center"><img src="https://latex.codecogs.com/png.latex?\bg_white&space;\fn_cm&space;TF(t)&space;=&space;\frac{\text{Number&space;of&space;times&space;term&space;t&space;appears&space;in&space;a&space;document}}{\text{Total&space;number&space;of&space;terms&space;in&space;the&space;document}}" title="TF(t) = \frac{\text{Number of times term t appears in a document}}{\text{Total number of terms in the document}}" width=70%/></p><br>

</li>
<li>
<strong>IDF:</strong> Inverse Document Frequency, which measures how important a term is. While computing TF, all terms are considered equally important. However it is known that certain terms, such as "is", "of", and "that", may appear a lot of times but have little importance. Thus we need to weigh down the frequent terms while scale up the rare ones, by computing the following: <br><br>

<p align="center"><img src="https://latex.codecogs.com/png.latex?\bg_white&space;\fn_cm&space;IDF(t)&space;=&space;\log_{e}\frac{\text{Total&space;number&space;of&space;documents}}&space;{\text{Number&space;of&space;documents&space;with&space;term&space;t&space;in&space;it}}" title="IDF(t) = \log_{e}\frac{\text{Total number of documents}} {\text{Number of documents with term t in it}}" width=70%/></p><br>

for numerical stabiltiy we will be changing this formula little bit<br><br>

<p align="center"><img src="https://latex.codecogs.com/png.latex?\bg_white&space;\fn_cm&space;IDF(t)&space;=&space;\log_{e}\frac{\text{Total&space;number&space;of&space;documents}}&space;{\text{Number&space;of&space;documents&space;with&space;term&space;t&space;in&space;it}&plus;1}" title="IDF(t) = \log_{e}\frac{\text{Total number of documents}} {\text{Number of documents with term t in it}+1}" width=70%/></p><br>

</li>
</ul>

## Example

Consider a document containing 100 words wherein the word cat appears 3 times. The term frequency (i.e., tf) for cat is then (3 / 100) = 0.03. Now, assume we have 10 million documents and the word cat appears in one thousand of these. Then, the inverse document frequency (i.e., idf) is calculated as log(10,000,000 / 1,000) = 4. Thus, the Tf-idf weight is the product of these quantities: 0.03 \* 4 = 0.12.
