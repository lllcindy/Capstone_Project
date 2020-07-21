1. Package requirement:
sklearn
numpy
spacy

2. Download en_core_web_lg by command:
python -m spacy download en_core_web_lg

3. Functions

Similarity Detection Function:
1) diff_files(file_dir, ls):
    '''
    input:
    file_dir: directory of the 10k or 10Q files
    ls: list of 10k or 10Q file names, ordered by time decreasely,
    eg: ls = ['APPLE COMPUTER INC_19_10k.txt','APPLE COMPUTER INC_18_10k.txt',
              'APPLE COMPUTER INC_17_10k.txt'], compares apple 19 10k to 18 10k,
              then compares 18 10k to 17 10k

    output:
    similarity score list
    '''
2) diff_analysis(file1, file2, file1_suffix='', file2_suffix=''):
    '''
    Compare two files and output the similarity matrix
    '''

3) diff(sim, text_ls1, text_ls2, prefix_text1='', prefix_text2=''):
    '''
    compare text_ls1 with text_ls2
    mark different levels of similarity
    '''
4) getTFIDF(corpus):
    '''
    Get TFIDF matrix from the corpus
    '''
5) getCorpus(text_nlp, vocabulary=vocabulary):
    '''
    Get corpus
    '''
6) load(file):
    '''
    Load file and pass it into the spacy English model
    '''

Visualization for Similarity
1) matrix_mani(sim):
    '''
    Input matrix is pandas DataFrame
    Column is the sentence number of newer 10K, starting from 0
    Row is the sentence number of older 10K, starting from 0
    Data for each individual cell is the cosine similarity between two sentences marked by the column and row.
    
    Output are three python list:
    First list contains pairs of numbers as a small list, in each small list, the first number is the sentence number
    in the newer 10K, second number is the sentence number corresponding in the older 10K, and -1 stands for there is no match
    Second list contains several numbers which indicate in the newer 10K which sentence is added
    Third list contains several numbers which indicate form the older 10K which sentence is deleted
    '''
2) write_html(pairs, deletion, dic_1, dic_2, file1_suffix, file2_suffix, score):
    '''
    Write similarity pairs to HTML file
    '''
	
Visualization for Sentiment (included because similarity matrix is required as an input)
1) lemmatize_words(words):
    '''
    Lemmatize words 
    Returns lemmatized_words : list of str
    '''
2) build_dic():
	'''
	Build a dictionary based on LoughranMcDonald_MasterDictionary_2018.csv
	'''
3) build_dic_sent(file1, file2):
	'''
	from two input file, Filter specific sentences using sentiment dictionary
	'''
4) sent_html(dic_sent, dic_curr, dic_last, dic_1, dic_2, file1_suffix, file2_suffix):
    '''
    Write sentiment analysis word sentence pair to HTML file
    '''

4. demo to use functions to do similarity analysis
'''
Common function:
get files from a directory and organize the files by company names,
then detect similarity by companys in time reversed order.
'''
# file_dir = r'/content/drive/My Drive/Capstone_file/
file_dir = r'/content/drive/My Drive/Capstone_file/date_version'
ls = [f for f in os.listdir(file_dir) if '.txt' in f]
d  = dict()
for file in ls:
    company = file.split('_')[0]
    d[company] = d.get(company, []) + [file]


for company in d:
    ls = sorted(d[company])[::-1]
    # print(ls)
    diff_files(file_dir, ls)