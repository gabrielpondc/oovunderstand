# Chinese OOV recognition and understanding by contextual Word2Vec model
### Content
### Project Introduction
The aim of this project is to discover OOV(out of vocabulary) from Sina Weibo and to understand OOV by using the Word2Vec model. The first step was generated word lists through Mutual information and Left and Right Entropy Measures from news corpus of Sina Weibo was crawled, and OOV was extracted from the word lists through online dictionaries. The second step was extracted the relevant corpus containing OOV from Weibo. The third step, a third-party tool was used to divide the corpus into words and to obtain the distributed representation of words using Word2Vec's CBOW(continues bag of word) and Skip-Gram models. The fourth step was distributed representation information is used to compute words that are similar to the OOV in order to achieve semantic understanding of the OOV.The final result model has a high rate of correct word comprehension and is able to understand most of the OOV. 
***
### Run Way
    Mining the data for the corpus
    $python weibomining.py
    Extract the word from corpus as word list
    $python oovfinder.py
    Compare the word list with dictionary and extract the oov as list
    $python isoov.py
    Filter person name , organization name , place name from OOV list and delete these word from the list as cleaned oov list
    $python namefinder.py
    $python placefinder.py
    $python orgfinder.py
    Mining some corpus using the oov as keyword in Weibo 
    $python keywordcorpuscrawl.py
    Merge the keyword corpus and origin corpus and spilt words with jieba
    $python splitsystem.py
    Training model and caculate the similarity of each oov
    $python modeltraining.py
***
### Dependencies
    > python 3.9
    > jieba
    > requests
    > lxml
    > gensim
    > sklearn
    > matplotlib
***
### Data source
Corpus www.weibo.com/breakingnews
Dictionary https://hanyu.baidu.com/
