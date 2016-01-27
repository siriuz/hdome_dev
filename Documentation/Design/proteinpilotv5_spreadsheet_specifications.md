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

This field contains the UniProt codes identifying the Protein. It is allowed to contain more than one element, delimited by ';'. Each element is parsed separately.  
The actual UniProt ID key that is stored is the string between the '|', i.e Q9BY89 and P09230 here.  
This key is stored as a string in the `Protein` entity under the `prot_id` attribute with each element having its own instance of `Protein`.  


### Names
> Uncharacterized protein KIAA1671 OS=Homo sapiens GN=KIAA1671 PE=1 SV=2  
> Alkaline extracellular protease OS=Yarrowia lipolytica (strain CLIB 122 / E 150) GN=XPR2 PE=1 SV=1  

Data field identifier: **proteins**  
This field contains the names of the Proteins. This field is allowed to have multiple elements in it, delimited by ';'.  
Each of these elements are stored as a separate `Protein` entity, and the string is stored in the `description` attribute.   


### Conf
> 99.0000009536743  

Data field identifier: **confidence**  
This field contains the confidence level of the identification and is used to compare against the experiment cutoff confidence level.  
The field is converted into a float, rounded to 5 decimal places
This value is then stored in the `IdEstimate` entity under the `confidence` attribute as a float.


### Sequence
> MPGLVGQEVGSGEGPR  
> LATAFTILTAVLAAPLAAPAPAPDAAPAAVPEGPAAAAYSSILSVVAKQSK  

Data field identifier: **peptide_sequence"  
This field contains the sequence of the Protein or Peptide that was identified by ProteinPilot  
The field is not parsed in any way, and it is stored as a string in the `Peptide` entity under the `sequence` attribute.


### Modifications
> Deamidated(Q)@7  

Data field identifier: **ptms**  
This field denotes the modifications to the procedure made in the experiment.  
As with the `protein` and `names` field, this can have multiple elements delimited by ';'. Each one is stored as a separate instance of the `Ptm` entity inside the `description` field.   


### dMass
> -0.0842337981  
> -0.1522669941  

Data field identifier: **delta_mass** 
This field may not contain multiple elements. It is converted into a float then rounded to 5 decimal places 
This value is then stored in the `Ion` entity, in the `delta_mass` attribute as a float.  


### Prec MW
> 1569.6614990234  
> 4810.4985351563  

Data field identifier: **precursor_mass**  
This field may not contain multiple elements. It is converted into a float then rounded to 5 decimal places 
This value is then stored in the `IdEstimate` entity, in the `precursor_mass` attribute as a float.  


### Prec m/z
> 785.838  
> 1203.632  

Data field identifier: **mz**  
This field may not contain multiple elements. It is converted into a float then rounded to 5 decimal places 
This value is then stored in the `Ion` entity, in the `mz` attribute as a float.  


### Theor z
> 2  
> 4  

Data field identifier: **charge**  
This field may not contain multiple elements. It is stored in the `Ion` entity in the `charge_state` attribute without any further parsing.  


### Spectrum
> 1.1.1.5184.2  
> 1.1.1.9519.2  

Data field identifier: **dataset_id**, **spectrum**  
This field is parsed to populate two fields - the first numeric element before the '.' is used to populate the "dataset #<number>" portion of the `title` attribute in the `Dataset` entity.
The whole field is also imported as a string to populate the `spectrum` attribute in the `Ion` entity. This attribute seems to be optional according to the Django model.


### Time
> 24.3733  
> 47.3058  

Data field identifier: **retention_time**  
This field is NOT rounded to 5 decimal places! It is imported straight into the `retention_time` field in `Ion`.
