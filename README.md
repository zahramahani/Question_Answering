# Question Answeing
trying to find entities with the help of deeplearning in python(bert) and wikipedia.
## description of dataset 
data set is made of tripels (with inspiration of rdf) each triples contains :<br/> from_entity:the title of article(page) of wikipedia.<br/>
sentence:the sentence which is in the article (the connector).<br/> to_entities: which is the set of entities that are exists in the sentence.<br/>
## first step: making data set 
for this step we got the latest wikipedia dump  which contains 5,400,000 articles.<br/>
we got enwiki-latest-pages-articles.xml.bz2 from [link](https://dumps.wikimedia.org/enwiki/latest).<br/>  
then we extracted:title,interlinks,and sections of each article and wrote it in a line per article with the help of [gensim](https://radimrehurek.com/gensim/scripts/segment_wiki.html).<br/> 
the result of gensim processing named enwiki-latest.json.gz which we will use it in datasetMaking.ipynb. <br/> <br/>
for making our data set we also need to know all entities of each mention to find entities which are repeated in the article but there is no link for them because of avoidance of reputation.we took this set from resources of [Reimplimentation of Tagme](https://github.com/fedenanni/Reimplementing-TagMe).<br/>
we used [mention_overall_dict.pickle](https://drive.google.com/drive/folders/1lcq0PRRq8o_G-L-pQrV7GG-Btn-xPFlr)<br/>
## second step: linking sentence to entities(from_entity-to_entity)
for this work we first used transformer [example code](https://www.tensorflow.org/tutorials/text/transformer) from tensorflow and gave our own data set instead.


