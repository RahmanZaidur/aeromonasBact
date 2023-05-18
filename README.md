Hypothetical Protein prediction of Aeromonas hydrophile Bacterium

File Description

go_parent_data.csv - This the database containing all the level 2 ancestors of the go terms. These are collected manually from the uniprot website

uniprot_df.csv - fasta sequences are pulled from Uniprot Database (www.uniprot.org) with search query "aeronomas" and selecting annotation score 3, 4 and 5. Downloaded sequences are compressed. Need to be decompressed using gzip.open. After decompressing, the three sequences are combined into uniprot_df and written to uniprot_df.csv

uniprot_df.fasta - fasta format of the file uniprot_df.csv

uniprot_go_childs - uniprot_df database with a column named go_terms. These are the children go terms pulled from uniprot using the sequence id.
