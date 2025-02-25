# README
# Prey selection by *Chordeiles minor* (Common Nighthawks) does not reflect differences in prey availability between breeding and nonbreeding grounds

## Description of the data and file structure

We examined the diets and prey communities of *C. minor* during two breeding seasons in Florida, USA, and two nonbreeding seasons in Corrientes Province, Argentina (2020–2022). We used DNA metabarcoding to identify insect prey in *C. minor* fecal samples, and we employed malaise and UV light traps to assess the abundance and composition of aerial insect prey communities. Demultiplexed sequences from fecal metabarcoding were processed in Qiime2, and analysis of diet diversity, prey selection, and insect community diversity was conducted in R using the scripts and data files contained in this directory.

### **Contents**

All raw data can be found in the data/ folder, saved model outputs in models/, and output tables in output/.

#### data/

all_taxa.csv

* (list of all insects detected in diet samples after filtering, given at the most precise level obtained via metabarcoding)

- Missing data: NA = was not classified at this level

* Columns
  * order: insect order ID
  * family: insect family ID
  * genus: insect genus ID
  * species: insect species ID

bold-taxonomy.qza 

* (sequence data classified using BOLD reference library)

- Needs to be read into R using 'qiime2R' function; this produces a list of objects including version and format info.

* Relevant sequence data is contained in [["data"]]

- Columns
  * "Feature.ID": uniqe identifier for ASV
  * "Taxon": complete taxonomic assignment
  * "Confidence": percent match to reference (proportion)

cust-taxonomy.qza

* (sequence data classified using custom reference library)
* Same structure as bold-taxonomy.qza

ncbi-taxonomy.qza

* (sequence data classified using NCBI reference library)
* Same structure as bold-taxonomy.qza

table-176-dada2.qza

* (processed sequence table exported from qiime2)
* Needs to be read into R using 'qiime2R' function; this produces a list of objects including version and format info.
* Relevant sequence data is contained in [["data"]]
  * Each row represents a unique ASV detected in diet (row names correspond with Feature.ID in *_taxonomy.qza files.
  * Each column represents a unique fecal sample. Samples starting with "CONI_2" are from USA and "CONI_RSM" are from Argentina.

qiime_metadata_coni.csv

* (sample metadata formatted for qiime2)

- Missing values: NA = not measured

* Columns
  * sample-id: Unique sample ID
  * source: location of sample collection (Citrus = Citrus WMA, RSM = Reserva NRSM)
  * dry-mass: mass of completely dried fecal sample (g) 
  * quality-ng-ul: DNA quality before PCR1 (nanograms per microliter)
  * sample-num: sample number, if more than one sample per bird
  * clean: yes/no; whether the sample was collected from a clean surface (yes) or not clean surface (no)
  * collect-date: sample collection date (m-d-yyyy)
  * source-year: site and year of collection (1 = first year, 2 = second year)
  * collect-time: sample collection time (hh:mm)
  * x-decimal-degree: longitude of sample collection (DD)
  * y-decimal-degree: latitude of sample collection (DD)

insect_data_arg_final.csv

* (raw data for insect trap samples in Argentina)

- Missing values: NA = not measured

* Columns
  * date: collection date (m/d/yyyy)
  * year: collection year
  * trap_id: unique sampling event ID
  * trap_type: trap type used for collection Malaise (M) or UV light (U)
  * length: insect body length (mm)
  * order: insect order
  * family: insect family

insect_data_fl_final.csv

* (raw data for insect trap samples in Florida)

- Missing values: NA = not measured

* Columns
  * date: collection date (m/d/yyyy)
  * year: collection year
  * trap_id: unique sampling event ID
  * trap_type: trap type used for collection Malaise (M) or UV light (U)
  * length: insect body length (mm)
  * order: insect order
  * family: insect family

#### models/

coni_null_m_arg.rda

* (prey selection econullnetr model output for Argentina Malaise trap data)
* data structure can be found in the the helpfile for generate_null_net()

coni_null_m_fl.rda 

* (prey selection econullnetr model output for Florida Malaise trap data)
* data structure can be found in the the helpfile for generate_null_net()

coni_null_u_arg.rda 

* (prey selection econullnetr model output for Argentina UV trap data)

- data structure can be found in the the helpfile for generate_null_net()

coni_null_u_fl.rda 

* (prey selection econullnetr model output for Florida UV trap data)

- data structure can be found in the helpfile for generate_null_net()

insect.dissim.arg.csv

* (insect community dissimilarity model output for Argentina)

- data structure can be found in the helpfile for iNEXT.beta3D()

insect.dissim.fl.csv 

* (insect community dissimilarity model output for Florida)

- data structure can be found in the helpfile for iNEXT.beta3D()

insect.diversity.arg.csv 

* (insect community diversity model output for Argentina)

- data structure can be found in the helpfile for iNEXT.beta3D()

insect.diversity.fl.csv 

* (insect community diversity model output for Florida)

- data structure can be found in the helpfile for iNEXT.beta3D()

#### output/

Empty directory to house output files from R scripts

#### scripts/

R scripts should be run in order (from 1\_ to 3_)

coni_qiime2_scripts.txt

* (scripts for processing raw reads in qiime2)

1_coni_diet_sequence_processing.Rmd

* (R script for processing sequence data exported from qiime2)

2_coni_diet_diversity.Rmd

* (R script for diet diversity analysis)

3_prey_selection_diversity.Rmd

* (R script for prey selection and prey diversity analysis)

## Code/software

Qiime 2 2023.5

R 4.3.2

## Access information

Data for creating COI classifiers was derived from the following sources:

O'Rourke, D. R., N. A. Bokulich, M. A. Jusino, M. D. MacManes, J. T. Foster (2020). A total crapshoot? Evaluating bioinformatic decisions in animal diet metabarcoding analyses. *Ecology and Evolution* 00: 1– 19.

Robeson II, M. E., D. R. O’Rourke, B. D. Kaehler, M. Ziemski, M. R. Dillon, J. T. Foster, N. A Bokulich (2020). RESCRIPt: Reproducible sequence taxonomy reference database management for the masses. *bioRxiv* 10.05.326504.
