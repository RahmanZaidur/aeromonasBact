Hypothetical Protein prediction of Aeromonas hydrophile Bacterium

File Description

##
go_parent_data.csv - This the database containing all the level 2 ancestors of the go terms. These are collected manually from the uniprot website

##
uniprot_df.csv - fasta sequences are pulled from Uniprot Database (www.uniprot.org) with search query "aeronomas" and selecting annotation score 3, 4 and 5. Downloaded sequences are compressed. Need to be decompressed using gzip.open. After decompressing, the three sequences are combined into uniprot_df and written to uniprot_df.csv
1540 sequences had no go terms. Their entry was deleted from Uniprot. These sequences have been removed and file was updated.

##
uniprot_df.fasta - fasta format of the file uniprot_df.csv

##
uniprot_go_childs.csv - uniprot_df database with an additional column named go_terms. These are the children go terms pulled from uniprot using the sequence id. 1540 sequences had no go terms. Their entry was deleted from Uniprot. These sequences have been removed and file was updated.
There were 74 GO Terms in this file, which were obsolete and records were deleted. Those GO terms were removed with remove_obsolete_go_terms.ipynb file and file was updated.

##
go-basic.obo - latest version of the GO database in OBO format from the Gene Ontology website: http://geneontology.org/docs/download-ontology/
This is used to get the ancestors of the go terms

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
This text file is unstructured and need to be structured

##
extract_psortb_texts.ipynb - This code extracts the columns from psortb parsed text file - psort_parsed.txt, create dataframe and write it in a csv file called 'psort_extract_df.csv'

##
psort_extract_df.csv - the csv file containing the structured output of psort_parsed.txt file. It has 19 columns along with the main sequence id column.





