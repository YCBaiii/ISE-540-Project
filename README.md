# ISE-540-Project
ISE 540 Final Project - Financial Narratives: A Comprehensive Risk Analysis Tool

Overview:
In this project, we divide the codes into 5 sections: 
· Section 1: Datasets Downloads and Preparation
· Section 2: Risk Factor Extraction
· Section 3: Risk Factor Organizing
· Section 4: Corpus
· Section 5: Model

Section 1:
The section 1 mainly focuses on dataset download and preparation. In this project instruction, we are given financial statement datasets from the SEC (https://www.sec.gov/dera/data/financial-statement-data-sets). However, this dataset only contains numerical variables, which is not satisfied with a text analysis. Therefore, we need to find the financial report in text format and download it.

Firstly, we rewrite a Standard Industrial Classification (SIC) dataset. We find that in the original dataset provided in the instruction, there is a variable named SIC, which is an identifier of the industry. To figure out the meaning of each code, we find the explanation on SEC website (https://www.sec.gov/corpfin/division-of-corporation-finance-standard-industrial-classification-sic-code-list). In order to read the content as a dataframe later on, we copy the text from the website and save as a .txt file and we define a function to rewrite the SIC.txt file as a .csv file.

Secondly, we read in the original dataset from 2022Q1 up to now which is 2023Q3. For each dataset of a specified quarter, there are 4 .txt files which are number, presentation, submission, and tag. We only focus on the latest and complete year so we filter the records with a fiscal year of 2022. Because what we are interested in in this project is the risk and 10-K form always contains a section named "Risk Factors" we filter the 10-K form from the whole records. All of these 10-K forms could be downloaded from the SEC EDGAR system so we generate a URL to acquire the 10-K report.

Thirdly, We do some EDA to decide which industries are popular and download the corresponding 10-K file from the website. To be specific, the 5 industries we selected are bank, energy, life sciences, real estate, and technology service.



Section 2:
In the previous section, we have already downloaded the financial reports in HTML format .txt file. In this section, we extract the risk factors from these files and extract the subjects in these texts. Because we have already selected 5 industries. Our extraction performs on these industries separately, which corresponds to the codes of "Section 2.1" - "Section 2.5".

Basically, we separate the main body and find the keyword "Item 1. Risk Factors" as the start index and "Item 1B. Unresolved Staff Comments" as the end index to extract the risk factors section. We store them in the corresponding folder, for instance, for industry 6021 which is a bank industry, we store these files in a folder named "Risk Factor Text/Bank Industry/Industry_6021/Raw Text". Due to the difference in the title name, coding style, etc, our functions might not extract well in some of them.

In each risk factor, there are some titles written in bold, which are subjects we are going to use later on to perform our model. Similarly, we store these subjects in a corresponding folder, for instance, for industry 6021 which is a bank industry, we store these files in a folder named "Risk Factor Text/Bank Industry/Industry_6021/Subject".



Section 3:
In this section, we are just going to organize the subject .txt files into a .csv file. By the code "Section 3.1", we generate a form for each industry and store it in a folder named "Risk Factor Subject Text Summary". 

Based on the files we acquired, we manually label the risk categories of each subject and then we use "Section 3.2" codes to combine all of these forms named "risk.csv".



Section 4:
We mainly focus on building up some corpus for later use in this section. The code of "Section 4.1" is going to build up a corpus based on the risk factor text downloaded from the SEC. As we mentioned, we have generated a URL to download the financial reports. Here, we use the same way but download more files for our corpus. All of these original files are stored in a folder named "Downloaded Corpus". Using a similar technique in "Section 2.1" - "Section 2.5", we extract the subjects of the risk factors section from the text. However, due to the size of the original files, we have to divide them into 3 parts to process them separately and store them in a corresponding folder. For example, for a file in part 1, the subject would be stored in the folder named "Corpus Extraction/Part 1/Subject/". Then, we generate a .csv file for each of them and combine them together. Because there are some empty lines and incompleted lines in the .csv file, we need to remove them. Plus, we have already extracted subjects for some files in section 3 which could be used in the corpus as well. Therefore, we combine them together. Finally, we get a file named "Corpus.csv".

The code of "Section 4.2" is used to build up a corpus based on the Wikipedia corpus we downloaded at https://dumps.wikimedia.org/backup-index.html. Firstly, we need to transform the file into a .txt file so that we can use it later. Secondly, since the file we extracted are too large to process directly, we split them into small pieces. Note: Those Wikipedia corpus file are not saved here.



Section 5:
In this section, we make an EDA on our labeled dataset and train the word2vec model by two different corpus. In the code of "Section 5.1", the corpus we used is the Wikipedia corpus. In the code of "Section 5.2", the corpus we used is the risk factors corpus.
