# Question Answeing (CER)
trying to find question answer entities with the help of deep learning in python(bert), textual graph and wikipedia.


- creating textual graph.


- according to question input from DBpedia-v2, its related graph will extract.


- relating graph will prune.


- ranking of candidte answers of questin from DBpedia-v2 will be done.


for understanding more refer to our paper [Learning to Rank Knowledge Subgraph Nodes for Entity Retrieval](https://dl.acm.org/doi/10.1145/3477495.3531888)




## description of textual graph
### data set is made of tripels (with inspiration of rdf) each triples contains


**from_entity (head) :** the title of article(page) of wikipedia or an entity mention which exist with other entity mention co occured in the same sentence in any wiki page


**sentence:** the sentence which is in the article (the connector).


**to_entities (tail) :** which is the set of entities that are exists in the sentence.or an entity mention which exist with other entity mention co occured in the same sentence in any wiki page



## first step: creating textual graph 
for this step we got the latest wikipedia dump  which contains 5,400,000 articles.


we got enwiki-latest-pages-articles.xml.bz2 from [link](https://dumps.wikimedia.org/enwiki/latest).


then we extracted:title,interlinks,and sections of each article and wrote it in a line per article with the help of [gensim](https://radimrehurek.com/gensim/scripts/segment_wiki.html).


the result of gensim processing named enwiki-latest.json.gz which we will use it in **datasetMaking.ipynb**.


for making our textual graph we also need to know all entities of each mention to find entities which are repeated in the article but there is no link for them because of avoidance of reputation.we took this set from resources of [Reimplimentation of Tagme](https://github.com/fedenanni/Reimplementing-TagMe).


we used [mention_overall_dict.pickle](https://drive.google.com/drive/folders/1lcq0PRRq8o_G-L-pQrV7GG-Btn-xPFlr)




### example

here is a sample of data which is reterived for **[Berlin](https://en.wikipedia.org/wiki/Berlin)** page in wikipedia


#### **RED** entities, are tail of direct triples.
**direct triples** are triples which head entity is page title and tail entity is found in a sentence in that page.


#### **BLUE** entities, are head and tail of undirect triples.
**undirect triples** are triples which head entity and tail entity are found in the same sentence in a page.for each pair we make 2 triple, with changing head and tail. (not implemented in **datasetMaking.ipynb** sample code)


![](https://github.com/zahramahani/Question_Answering/blob/master/pics/simple_graph_sample_for_page_berlin.png)


## second step: using created textual graph to answer the question.
### [CER](https://dl.acm.org/doi/10.1145/3477495.3531888)
**CER** is a Contextual Entity Retrieval method that models contextual relationship between entities and effectively limits the extensive search space without compromising performance. In this method, a model is trained to prune an extracted subgraph from a textual knowledge graph that represents the relations between entities and then a second deep model is trained to rank entities in the subgraph by reasoning over the textual content of nodes, edges, and the given query.


### Code
we have provided our code in src section that can be used for producing the results. The extracted data from contextual Wikipedia knowledge graph for DBPedia-Entity v2 can be found here.

#### To run the code, place the downloaded file in data folder and run the following commands:
```
cd src\data\
bash split.sh
cd ..
bash run.sh

```

