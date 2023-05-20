Hypothetical Protein prediction of Aeromonas hydrophile Bacterium

File Description

go_parent_data.csv - This the database containing all the level 2 ancestors of the go terms. These are collected manually from the uniprot website

uniprot_df.csv - fasta sequences are pulled from Uniprot Database (www.uniprot.org) with search query "aeronomas" and selecting annotation score 3, 4 and 5. Downloaded sequences are compressed. Need to be decompressed using gzip.open. After decompressing, the three sequences are combined into uniprot_df and written to uniprot_df.csv

uniprot_df.fasta - fasta format of the file uniprot_df.csv

uniprot_go_childs.csv - uniprot_df database with an additional column named go_terms. These are the children go terms pulled from uniprot using the sequence id. 1540 sequences had no go terms. Their entry was deleted from Uniprot. These sequences have been removed and file was updated.
There were 74 GO Terms in this file, which were obsolete and records were deleted. Those GO terms were removed with remove_obsolete_go_terms.ipynb file and file was updated.

go-basic.obo - latest version of the GO database in OBO format from the Gene Ontology website: http://geneontology.org/docs/download-ontology/
This is used to get the ancestors of the go terms




