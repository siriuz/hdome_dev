#File Format

The spreadsheet is represented by a Tab delimited .csv file with 27 columns.

Each column may be further split into separate elements depending on the column specification which will be described in more detail below.

Deriving from the parsing code written by Kieran, it is not assumed that the columns are specified in a fixed order. This is inferred by the fact that there is a method which searches for keywords in the header (first row) of the .csv and then creates a mapping between data field identifiers and the respective column number.

# Columns

The heading of each section below is the keyword being matched. The code will match the keyword to a **data field identifier**.
If the column isn't specified below, it doesn't seem to be used in the import. (Refer to 'matchdict' in pepsite.uploaders)
Examples are displayed in the blockquotes
> Example

### Accessions
> sp|Q9BY89|K1671_HUMAN
> sp|P09230|AEP_YARLI

Data field identifier: **uniprot_ids**

This field contains the UniProt codes identifying the Protein or Peptide.
The actual UniProt ID key that is stored is the string between the '|', i.e Q9BY89 and P09230 here.
This key is stored in the `Protein` class under the `prot_id` attribute.

### Names
> Uncharacterized protein KIAA1671 OS=Homo sapiens GN=KIAA1671 PE=1 SV=2
> Alkaline extracellular protease OS=Yarrowia lipolytica (strain CLIB 122 / E 150) GN=XPR2 PE=1 SV=1

Data field identifier: **proteins**
This field contains the names of the Proteins

### Conf
> 99.0000009536743

Data field identifier: **confidence**
This field contains the confidence level of the identification and is used to compare against the experiment cutoff confidence level.

### Sequence
> MPGLVGQEVGSGEGPR
> LATAFTILTAVLAAPLAAPAPAPDAAPAAVPEGPAAAAYSSILSVVAKQSK

Data field identifier: **peptide_sequence"
This field contains the sequence of the Protein or Peptide that was identified by ProteinPilot

### Modifications
> Deamidated(Q)@7

Data field identifier: **ptms**

### dMass
> -0.0842337981
> -0.1522669941

Data field identifier: **delta_mass**

### Prec MW
> 1569.6614990234
> 4810.4985351563

Data field identifier: **precursor_mass**

### Prec m/z
> 785.838
> 1203.632

Data field identifier: **mz**

### Theor z
> 2
> 4

Data field identifier: **charge**

### Spectrum
> 1.1.1.5184.2
> 1.1.1.9519.2

Data field identifier: **dataset_id**

### Time
> 24.3733
> 47.3058

Data field identifier: **retention_time**
