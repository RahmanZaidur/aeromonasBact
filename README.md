Hypothetical Protein prediction of Aeromonas hydrophile Bacterium

File Description

##
go_parent_data.csv - This the database containing all the level 2 ancestors of the go terms. These are collected manually from the uniprot website

##
uniprot_df.csv - fasta sequences are pulled from Uniprot Database (www.uniprot.org) with search query "aeronomas" and selecting annotation score 3, 4 and 5. Downloaded sequences are compressed. Need to be decompressed using gzip.open. After decompressing, the three sequences are combined into uniprot_df and written to uniprot_df.csv. Total sequence number - 31,321

1540 sequences had no go terms. Their entry was deleted from Uniprot. These sequences have been removed and file was updated. Total Sequence Number - 29,781

5 sequences had "X" in them. X means unknown amino acid. X makes it difficult to get the Physicochemical features with biopython. Those 5 sequences were removed. Removed ids - ['Q9PRY2', 'P81903', 'Q03321', 'A0A428VHZ9', 'A0A1Q8F8M2']
Now total Sequence- 29,776

ID - "P86454" has no return in blast hits. It was removed
ID - "Q9PRY2" has 2 blast hits, but both has query coverage 94% (<100%). It was already removed from uniprot_df, because it had X in the sequence. So, total sequences now - 29,775

There are 86 unique GO terms, that makes 86 prediction classes


##
remove_seq_with_x.ipynb - code to remove the sequences which had "X" in them. X means unknown amino acid. After removing, uniprot_df.csv file was updated.

##
uniprot_df.fasta - fasta format of the file uniprot_df.csv

##
uniprot_go_childs.csv - uniprot_df database with an additional column named go_terms. These are the children go terms pulled from uniprot using the sequence id. 1540 sequences had no go terms. Their entry was deleted from Uniprot. These sequences have been removed and file was updated.
There were 74 GO Terms in this file, which were obsolete and records were deleted. Those GO terms were removed with remove_obsolete_go_terms.ipynb file and file was updated.

##
go-basic.obo - latest version of the GO database in OBO format from the Gene Ontology website: http://geneontology.org/docs/download-ontology/
This is used to get the ancestors of the go terms

##
go_ancestor.ipynb - Final code to get the ancestors of each child GO term. This will only select those ancestors that have the highest generation level and also are present in the go_parent_data database
Then the output dataframe was saved as go_ancestor_data.csv

##
go_ancestor_data.csv - File containing sequence id, sequence, child GO Terms, Ancestor GO Terms. Created from go_ancestor.ipynb script.

##
DEG_parser.ipynb - This code parse the DEG gene blast (blastP) data from http://origin.tubic.org/deg/public/index.php/index website. It loops through the protein sequences from uniprot_df database and parse the DEG output for bacteria, archaea and eukaryotes. The output of this code is saved in two csv files - uniprot_DEG_df.csv and DEG_df_parsed.csv
Actual code is run on NDSU CCAST Cluster. Cluster code file is deg_parse.py

##
uniprot_DEG_df.csv - uniprot_df database with only DEG data. Along with the "id" and "sequence" column, it has the MaxID (Highest Identity percent of all hits of each sequence) and totalHits (Total number of hits of each sequence) columns for Bacteria, Archaea and Eukaryotes

##
DEG_df_parsed.csv - This is a nested dataframe csv. It contains all the parsed DEG data with the sequence id. It has 4 columns - "id", "bacteria_df", "archaea_df" and "eukaryotes_df". The df columns contains dataframes which holds the whole DEG request page for each sequence. These inner dataframes are stored in JSON format, which needs to be read using json library.
This is file is moved to BackupAeromonas folder as it is too big to push to Github.

##
psort_parsed.txt - This is the text output file from parsing the PSORTb database for each sequence (29781) of uniprot_df.fasta file. PSORTb website - https://www.psort.org/psortb/index.html
I used docker image of PSORTb command line tool in my PC. Docker link - https://hub.docker.com/r/brinkmanlab/psortb_commandline/
Run the docker image in a container, then open new terminal window.
Run> chmod +x psortb
Run> ./psortb -i /Users/zaidur/Documents/Sequence_Project/aeromonasBact/test_data_prep/test_df.fasta -r /Users/zaidur/Documents/Sequence_Project/aeromonasBact/test_data_prep/ --negative

This text file is unstructured and need to be structured

##
extract_psortb_texts.ipynb - This code extracts the columns from psortb parsed text file - psort_parsed.txt, create dataframe and write it in a csv file called 'psort_extract_df.csv'

##
psort_extract_df.csv - the csv file containing the structured output of psort_parsed.txt file. It has 19 columns along with the main sequence id column.

##
psort_scrapping.ipynb - This code is to extract PSORTb results directly from website using single fasta sequence.

##
psort_blast_scraping - This script automates the process of sending protein sequence data to the PSORTb database (https://db.psort.org/search/blast) and retrieving the prediction results. The input is a FASTA file containing protein sequences. For each sequence, the script sends a HTTP POST request to the PSORTb database with the protein sequence data. There are multiple hits for each sequence with different identity percentage. This code parses all the hits to extract relevant information.
This database is slightly different then (https://www.psort.org/psortb/index.html), as this provides matched hits using blast algorithm. And the other one provides summerized result for input sequence

##
physicochemical_feature_collector.ipynb - Protein Feature Extraction Script.
This script extracts various protein physiochemical features from uniprot_df dataframe of the protein sequences using the BioPython and ProPy libraries. It computes features such as molecular weight, instability index, isoelectric point, GRAVY, secondary structure fraction, grouped amino acid composition, and composition, transition, and distribution descriptors. The extracted features are then combined into a new DataFrame (features_df), which includes the 'id' column from the original DataFrame for easy reference. The dataframe is saved in a csv file called features_df.csv

Some sequence my have "X" (unknown amino acids) in them. Those sequence were identified and removed with remove_seq_with_x.ipynb

##
features_df.csv - the csv file containing the physiochemical features of the protein sequences. It has one column with the original sequence id and other columns are for the features. It has 29776 sequences.

##
blast_df_original.csv - contains 8941896 blast hits from 29780 sequences. Originally passed 29781 sequences, but sequence ID "P86454" did not have any hit.
File was prepared combining 6 log files from ccast job output.
This file is too large to push to github. So I kept it unstaged.

##
blast_feature_df.csv - From all the 8941896 blast hits of blast_df_original.csv file, unique IDs are separated. And for each unique ID, the number of hits with "query coverage">=100% and "identity percent">=80% were counted. The counts are in "count_blast" column and the average identity percents of those matches are in "AvgIdBlast" column.

ID 'Q9PRY2' was removed because, the query has lower query coverage.

Other 4 sequence IDs were removed to match up with the updated uniprot_df. Total sequence now is 29775

##
blast_feature_extraction.ipynb - This script is used to create the blast_df_original.csv file from the blast output log files.
Also, required "count_blast" and "AvgIdBlast" features are extracted to create blast_feature_df.csv file
The code has alternate filter methods, to apply on hypothetical test data, that are commented out.

##
DEG_Psort_features.csv - CSV file of the DEG and Psort Features along with the original ID and Target Go Terms.
Being a categorical column, "Final Prediction" column is converted into binary columns of the categories.
Also, the target go terms column is also encoded with one-hot encoding and converted into binary columns
The sequence number is matched up with latest uniprot_df. Total number of sequences - 29775

##
merge_deg_psortb_goTerms.ipynb - Using this script, DEG, Psortb and GO terms files are merged and created DEG_Psort_features.csv file.
The multi-label target column is encoded with one-hot encoding and created binary columns
The Final Selection columns is also one-hot encoded.

##
Feature Distribution - out of total 195 features ->
Physicochemical - 176 (column 0 - 175)
NCBI Blast - 2 (column 176 - 177)
DEG - 6 (column 178 - 183)
Psortb - 11 (column 184 - 195) [originally it had 6 columns, the last categorical column was encoded into 6 binary columns]

##
merged_df.csv - final encoded dataset with the id column

##
merged_df_final.csv - final encoded dataset without the id column. Ready for machine learning application

##
random_forest_model.ipynb - Code to merge the final dataset with all the features and training with Random Forest Classifier
This code first merge all the feature files (DEG, PSORTb, blast, pysiochemical) together based on the id.
Target columns are the leftmost 86 columns. The final dataset is saved in a csv file.
Then Multioutput Random Forest is applied on the dataset after scaling the feature values.
Common accuracy metrices are shown for the model prediction.

Also a function is defined to find out the class labels (GO Terms) of the predictions. And Another function was defined to find out the description of the class labels (GO Terms Description) of the predictions

##
randomForest_100_42.pkl - pickle file containing the trained "random forest" model with with model paramater, n_estimators=100, random_state=42






