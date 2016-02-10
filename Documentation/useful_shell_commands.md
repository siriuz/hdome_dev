# Useful shell commands for processing ProteinPilot files
A collection of little utilities I've written along the way and might come in useful at some point in the future.  
Due to the fact that some columns (Protein, Ptm, etc) can contain multiple entities, 
a common fragment seen in the below snippets is `sed 's/; /\n/g'`.  
This fragment replaces `; ` with a newline to split the entities each on their own line.
`sort -u` shows only one instance of a line even if there are duplicate lines in the file.  
You can append `wc -l` after that to count the number of rows output to get the unique entity count.

### All unique Accessions in a ProteinPilot file  
``` bash
awk -F '\t' 'NR>1 {print $7}' test_protein_pilot_v5_spreadsheet_long.txt | sed 's/; /\n/g' | sort -u
```
### All unique Protein Descriptions in a ProteinPilot file
``` bash
awk -F '\t' 'NR>1 {print $8}' test_protein_pilot_v5_spreadsheet_long.txt | sed 's/; /\n/g' | sort -u
```

### All unique Ptms in a ProteinPilot v5 file  
``` bash
awk -F '\t' 'NR>1 {print $14}' test_protein_pilot_v5_spreadsheet_long.txt | sed 's/; /\n/g' | sort -u
```

### All unique Peptide sequences in a ProteinPilot v5 file
``` bash
awk -F '\t' 'NR>1 {print $13}' test_protein_pilot_v5_spreadsheet_long.txt | sort -u
```

### Number of unique Ions (as defined by precursor mass, mz, theor z, and retention time)
``` bash
awk -F '\t' 'NR>1 {print $18, $19, $22, $25}' test_protein_pilot_v5_spreadsheet_long.txt | sort -u | wc -l
```
