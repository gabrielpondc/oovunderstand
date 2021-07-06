# Chinese OOV recognition and understanding by contextual Word2Vec model
### Content
### Project Introduction
The aim of this project is to discover OOV(out of vocabulary) from Sina Weibo and to understand OOV by using the Word2Vec model. The first step was generated word lists through Mutual information and Left and Right Entropy Measures from news corpus of Sina Weibo was crawled, and OOV was extracted from the word lists through online dictionaries. The second step was extracted the relevant corpus containing OOV from Weibo. The third step, a third-party tool was used to divide the corpus into words and to obtain the distributed representation of words using Word2Vec's CBOW(continues bag of word) and Skip-Gram models. The fourth step was distributed representation information is used to compute words that are similar to the OOV in order to achieve semantic understanding of the OOV.The final result model has a high rate of correct word comprehension and is able to understand most of the OOV. 
![image](https://github.com/gabrielpondc/oovunderstand/blob/main/result/1.png)
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
    Additional experiments are inputting an OOV for direct semantic understanding
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
<a href="https://www.weibo.com/breakingnews"><img src="https://img.shields.io/badge/Corpus Source-Sina Break News-brightgreen"></a>
<a href="https://hanyu.baidu.com/"><img src="https://img.shields.io/badge/Dictionary Source-Baidu Hanyu Dictionary-brightgreen"></a>
***
### Some Result
The example of ’凤凰网‘(Media organization)on the left and ‘新冠’(Covid-19) on the right,Because the word ‘凤凰网’ often appears in the back of some news, it is difficult to predict the meaning of the word because there is not enough information in the context and there is a lot of noise,On the contrary, the word '新冠' is rich in contextual information, so the predicted value is also relatively accurate.
![image](https://github.com/gabrielpondc/oovunderstand/blob/main/result/2.png)
This example shows the understand of '耗子尾汁' by both CBOW and Skip-gram models. Both models accurately understand the semantic words, but the similarity between the two words understood by the CBOW model is higher
![image](https://github.com/gabrielpondc/oovunderstand/blob/main/result/3.png)
![1](http://latex.codecogs.com/svg.latex?Accuracy%3D%5Cfrac%7B(A%2BB)%7D%7Bn%7D%5Ctimes100%5C%25)  
| Model | A | B | C |Accuracy|
| --- | --- | --- |--- |--- |
|CBOW  | 21 | 13 | 1|97.10%|
| Skip-gram | 17 |14  | 4|88.57%|  

***
### About the Author
JiaKai Gu  
E-mail: gabrielpondc@cau.ac.kr  
Jason J. Jung   
Department of Computer Engineering, Chung-Ang University 84, Heukseok-ro, Dongjak-gu, Seoul, Republic of Korea 06974  
Tel.: +82-2-820-5136  
Fax: +82-2-820-5301  
E-mail: j3ung@cau.ac.kr  

