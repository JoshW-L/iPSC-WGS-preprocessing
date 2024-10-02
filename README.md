# iPSC-WGS-preprocessing
Glioma Parental vs iPSC

This document will explain what I have done, what I have copied over and what needs to be repeated.

Samples are split into 3. 
The first are Healthy WGS's from 2 patients:
  1. NEBTR1
  2. LGGR1
     
The second is the original glioma tumour:
  1. L-R1-P
  2. G-R1-P
  3. N-R1-P

The third is the iPSC from the glioma tumour:
  1. L-R1-P
  2. G-R1-P
  3. N-R1-P

L is from a patient with low-grade glioma (LGG) and is mathced to the healthy LGGR1 WGS.
G and N is from a glioblastoma patient and is matched to the healthy NEBTR1 WGS.
G is from the bulk zone of the glioblastoma.
N is from the marginal zone of the glioblastoma.

First thing is to explain the fastq files thay can be located here:
https://leeds365-my.sharepoint.com/:f:/g/personal/bs23jmw_leeds_ac_uk/EvmTqLDOlOpGv77lcJGHWe4BON_BxZJ5PBaqvpqpP76oLQ?e=6qHKK8

Here there are 2 directories. The first (blood) contains the patients healthy WGS information. LGGR1 is the patient low grade glioma healthy WGS. The WGS was done using paired sequeencing hence the presence of R1 and R2. The second patient (NEBTR1) is the background for both the GBMR1 and NEBTR1 samples.

The second directory (brain) contains the parental tumour and iPSC for each patient. There are three repliactes in each sample, except in N-R1-P, where there aree four.

I ran QC, trimmed and QC'd these fastq files using bash scipts located here:
https://leeds365-my.sharepoint.com/:f:/g/personal/bs23jmw_leeds_ac_uk/EjhtJqSi775Bv-d0YjLSxLwBDIyozqKeqS93To-23IneXQ?e=7K3zSL

After this, I performed alignment using BWA. For this it is to be noted that the @RG needs to be included in the sam files. I have a tempate that needs some work. So please improve on this located here:
https://leeds365-my.sharepoint.com/:f:/g/personal/bs23jmw_leeds_ac_uk/Ene9ilOXnV1AlHQlaueZOlwBT0UYqqtTHfW7HU7UWmJg2g?e=iYdTyh

Alignment requires reference genome that can be found here:
https://leeds365-my.sharepoint.com/:f:/r/personal/bs23jmw_leeds_ac_uk/Documents/ARC4/WGS/Data/Alignment/Reference?csf=1&web=1&e=SdHKOC

Next you can run bam alignment to convert sam files into bam:


Then you have an option to concatenate the replicates into one for each sample. To do that I used these bash scripts:


Then you can finally run VCF. To do that you need GATK. Good information about this tool is here:
https://gatk.broadinstitute.org/hc/en-us/articles/360036194592-Getting-started-with-GATK4 

And Mutect2 is what you need:
https://gatk.broadinstitute.org/hc/en-us/articles/27007991962907-Mutect2

I downladed this tool and kept it in my tool directory:

Then you need this version of java to run it:

Finally you need to get a panel of normals and 
