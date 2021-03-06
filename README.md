# Chinese OOV recognition and understanding by contextual Word2Vec model
 <a href="https://github.com/topics/python"><img src="https://img.shields.io/badge/-Python-black?style=flat&logo=python&logoColor=white"></a>  [![GitHub issues](https://img.shields.io/github/issues/gabrielpondc/oovunderstand)](https://github.com/gabrielpondc/oovunderstand/issues)
### Content
- [Chinese OOV recognition and understanding by contextual Word2Vec model](#Chinese-OOV-recognition-and-understanding-by-contextual-Word2Vec-model)
    + [Project Introduction](#Project-Introduction)
    + [Run Way](#Run-Way)
    + [Word Extract](#Word-Extract)
    + [Some Result](#Some-Result)
    + [About the Author](#About-the-Author)
    + [Data source](#Data-source)
### Project Introduction
![image](https://github.com/gabrielpondc/oovunderstand/blob/main/result/1.png#pic_center)
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
### Word Extract
Mutual information(MI)   
![image](http://latex.codecogs.com/svg.latex?MI(x%3By)%3Dlog%5Cfrac%7Bp(x%2Cy)%7D%7Bp(x)p(y)%7D%3Dlog%5Cfrac%7Bp(x%7Cy)%7D%7Bp(x)%7D%3Dlog%5Cfrac%7Bp(y%7Cx)%7D%7Bp(y)%7D%5C)  
Higher the correlation between X and Y, the higher the possibility of X and Y forming words,Lower the value of mutual information, lower the correlation between X and Y, the higher possibility of a boundary between X and Y     
Left and right entropy   
![image](https://latex.codecogs.com/svg.latex?E_L%5Cleft(W%5Cright)%3D-%5Csum_%7B%5Cforall%20a%5Cin%20A%7D%7BP%5Cleft(aW%5Cmiddle%7C%20W%5Cright)%5Cast%7Blog%7D_2P%5Cleft(aW%5Cmiddle%7C%20W%5Cright)%7D)      
![image](https://latex.codecogs.com/svg.latex?E_R%5Cleft(W%5Cright)%3D-%5Csum_%7B%5Cforall%20b%5Cin%20B%7D%7BP%5Cleft(Wb%5Cmiddle%7C%20W%5Cright)%5Cast%7Blog%7D_2P%5Cleft(Wb%5Cmiddle%7C%20W%5Cright)%7D)   

W : candidate words after N-Gram segmentation.   
A: a collection of all words appearing on the left of a candidate.   
a: a word appearing on the left.   
B: a collection of all words appearing on the right of a candidate.   
b: a word appearing on the right.   
The more words appear around the candidate word W, the more likely it is that W is a word.    

***
### Some Result
|Class| OOV | Similar Words of OOV|
|:-:|:-:|:-:|
|A|?????????(Genius Disease)|?????????????????????(Asperger's Syndrome)
|B|?????? (COVID-19)|??????(Infection), ??????(Virus), ??????(pneumonia)
|C|?????????(Media Organization)|?????? (Should be),?????? (discuss),?????? (view)
***
The example of ???????????????(Media organization)on the left and ????????????(Covid-19) on the right,Because the word ??????????????? often appears in the back of some news, it is difficult to predict the meaning of the word because there is not enough information in the context and there is a lot of noise,On the contrary, the word '??????' is rich in contextual information, so the predicted value is also relatively accurate.
![image](https://github.com/gabrielpondc/oovunderstand/blob/main/result/2.png)
This example shows the understand of '????????????' by both CBOW and Skip-gram models. Both models accurately understand the semantic words, but the similarity between the two words understood by the CBOW model is higher
![image](https://github.com/gabrielpondc/oovunderstand/blob/main/result/3.png)
![1](http://latex.codecogs.com/svg.latex?Accuracy%3D%5Cfrac%7B(A%2BB)%7D%7Bn%7D%5Ctimes100%5C%25)  
| Model | A | B | C |Accuracy|
|:-:|:-:|:-:|:-:|:-:|
|CBOW  | 21 | 13 | 1|97.10%|
| Skip-gram | 17 |14  | 4|88.57%|  
***
The result of OOV ??? ???????????????
|Word| Translation| Similarity|
|:-:|:-:|:-:|
|???????????? |Take care of yourself| 0.99997896
|???| particle (in Chinese)| 0.99997878
|???| i| 0.99997693|
|????????? |Baoguo Ma |0.99997658|
|??? |Also |0.99997264|
|???| and |0.99997222|
|??? |particle (in Chinese)| 0.99997193|
***
### About the Author
JiaKai Gu   <a href="https://github.com/gabrielpondc"><img src="http://img.shields.io/badge/-Github-FFFFFF?style=flat&logo=github&logoColor=000000"></a>    
E-mail: gabrielpondc@cau.ac.kr  
Jason J. Jung   
Department of Computer Engineering, Chung-Ang University 84, Heukseok-ro, Dongjak-gu, Seoul, Republic of Korea 06974  
Tel.: +82-2-820-5136  
Fax: +82-2-820-5301  
E-mail: j3ung@cau.ac.kr  
### Data source
<a href="https://www.weibo.com/breakingnews"><img src="https://img.shields.io/badge/Corpus Source-Sina Break News-brightgreen"></a>
<a href="https://hanyu.baidu.com/"><img src="https://img.shields.io/badge/Dictionary Source-Baidu Hanyu Dictionary-brightgreen"></a>
***
