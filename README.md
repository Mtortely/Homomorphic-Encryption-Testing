# Homomorphic-Encryption-Testing

Homomorphic Encryption (HE) is a form of encryption that permits operations on ciphertexts, generating an encrypted result that, when decrypted, matches the result of operations performed on the plaintext. Previous research into HE has offered promising advancements in maintaining data privacy and security in areas such as managing suspicious persons lists in terms of accuracy, but the same challenges are brought up time and time again, computational overhead and system integration. I would like to focus on the computation aspect.
This report explores testing performed using HE on a synthetic dataset replicating finding information within a suspicious persons list context with varying data types and scale to observe if, and how these factors influence performance.

Overview
To eliminate as many external factors affecting the performance, I designed this test to be as simple and narrow as possible. I started by finding a synthetic dataset of transactions (Imranp 2018) with details such as amounts being sent, name of sender and name of receiver. The concept of the test was I had a suspicious persons list with one name on it, and I wanted to use HE to traverse through the dataset to see if the name was present. In practise, SP lists will be larger than one person, but this test aims to set baseline figures that can be built upon. 

Searches will be performed individually on both string data type (destination name column) and integer (destination balance before transaction to replicate phone numbers which would be in a SPL). The entire search process will be timed. It must be noted that the timing in this test does include the encryption process, so further testing can be performed to exclude this. The same dataset will be used for all the testing, with parameters that allow me to set the size of entries being targeted.
Framework/Library Choice
As search functionality once encrypted is the core concept of the project, partially homomorphic encryption was determined to be the best fit as the mathematical aspect allowed to me to perform the calculation ‘does a = b in dataset.’ I found the python 3 paillier PHE library to be the simplest and most efficient for the testing. 

Variables
Testing will be performed on the following entry sizes to replicate a range of small to large datasets:
 
•	10
•	50
•	100
•	500
•	1,000
•	5,000
•	10,000
•	50,000
•	100,000

 
I will be evaluating both true and false search queries in the respective data types:
 
String / true: 
 
String / false:
 
Int / true:
 
Int / false:
 

 
Dataset used 
https://www.kaggle.com/code/imranp/starter-synthetic-financial-datasets-cd6449a6-6/notebook 

Test Results
Time taken to perform search using HE (sec):
Entries 		Str / T		Str / F		Int /T		Int / F	
10		4	-	4	-	4	-	4	-
50		13	-	15	-	13	-	14	-
100		23	-	23	-	21	-	22	-
500		   108	1m 48s	107	1m 47s	108	1m 47s	108	1m 48s
1,000		224	3m 44s	221	3m 41s	222	3m 42s	222	3m 44s
5,000		1049	17m 29s	1058	17m 38s	1053	17m 33s	1051	17m 31s
10,000		2081	34m 41s	2074	34m 34s	2068	34m 28s	2080	34m 40s
50,000		10440	2h 54m	10238	2h 50m	10445	2h 54m	10347	2h 52m
100,000		20963	5h 49m	21004	5h 50m	20777	5h 46m	21010	5h 50m

 
Analysis
•	Data type did not affect the time taken to perform the search as results were consistent across all tests.
•	True/False search queries also did not affect the time taken as these results were just as consistent.
•	Even though I was performing the search on only one column, the rate at which the time taken increased was still exponential as I increased the number of entries that were being searched through. This does highlight how intense the computational needs get as we scale up.
•	I had to stop testing at 100,000 as the tests were taking way too much time/power. Considering the original dataset that I chose had well over 1,000,000 entries, (which is common for datasets), I calculated that it would have taken approx. 50hours + to compute.

Conclusion
For Homomorphic Encryption to be considered in financial settings, future research needs to be done into optimizing HE algorithms and/or enhancing system efficiency. While the accuracy offered in combination with the privacy-preserving nature of the algorithms are sought after, the exponential rate at which current HE algorithmic approaches grow in resources/time needed to perform are not suitable for practical applications such as managing suspicious persons lists at scale. 
