# Question Answeing
trying to find entities with the help of deeplearning in python(bert) and wikipedia.
## description of dataset 
#### data set is made of tripels (with inspiration of rdf) each triples contains :<br/><br/>

**from_entity:** the title of article(page) of wikipedia or an entity mention which exist with other entity mention co occured in the same sentence in any wiki page<br/><br/>

**sentence:** the sentence which is in the article (the connector).<br/><br/>

**to_entities:** which is the set of entities that are exists in the sentence.or an entity mention which exist with other entity mention co occured in the same sentence in any wiki page<br/>
## first step: making data set 
for this step we got the latest wikipedia dump  which contains 5,400,000 articles.<br/>
we got enwiki-latest-pages-articles.xml.bz2 from [link](https://dumps.wikimedia.org/enwiki/latest).<br/>  
then we extracted:title,interlinks,and sections of each article and wrote it in a line per article with the help of [gensim](https://radimrehurek.com/gensim/scripts/segment_wiki.html).<br/> 
the result of gensim processing named enwiki-latest.json.gz which we will use it in datasetMaking.ipynb. <br/> <br/>
for making our data set we also need to know all entities of each mention to find entities which are repeated in the article but there is no link for them because of avoidance of reputation.we took this set from resources of [Reimplimentation of Tagme](https://github.com/fedenanni/Reimplementing-TagMe).<br/>
we used [mention_overall_dict.pickle](https://drive.google.com/drive/folders/1lcq0PRRq8o_G-L-pQrV7GG-Btn-xPFlr)<br/>
## second step: using created dataset with the help of elastic search to answer the question.
### [CER](https://dl.acm.org/doi/10.1145/3477495.3531888)
#### **CER** is a Contextual Entity Retrieval method that models contextual relationship between entities and effectively limits the extensive search space without compromising performance. In this method, a model is trained to prune an extracted subgraph from a textual knowledge graph that represents the relations between entities and then a second deep model is trained to rank entities in the subgraph by reasoning over the textual content of nodes, edges, and the given query.


## Code
#### we have provided our code in src section that can be used for producing the results. The extracted data from contextual Wikipedia knowledge graph for DBPedia-Entity v2 can be found here.

#### To run the code, place the downloaded file in data folder and run the following commands:
```
cd src\data\
bash split.sh
cd ..
bash run.sh

```

