# Core Bioinformatics Resources
The repo is intended as a collection of the resources that are available through the Core Bioinformatics at NYUAD.

Here, you will find information on:

- The Core Bioinformatics team members, the organisation of the team, and their areas of expertise.
- How to interact and get in touch with the team, and raise specific requests.
- The data SOPs (archiving and retrieval of data, sharing of data, and submission of data to public repositories).
- Using the inhouse LIMS (Laboratory Information Management System) and submitting samples for sequencing.
- Primary sequence analysis using GURU (Genomics seqUencing Run aUtomation).
- Project management using JIRA.
- Downstream analysis using NASQAR.
- The in-house developed Workflow management system BioSAILs and the production level YAML workflows available.
- Bioinformatics software ecosystem on the NYUAD HPC cluster Jubail (GENCORE modules).


## The Team

The Core BioInformatics at New York University Abu Dhabi was established to provide a nexus for cutting-edge life sciences research in the United Arab Emirates, with world-class facilities and resources to promote innovative advances in genomics and systems biology.

Our focus is to provide computational infrastructure and services for sequence analysis in support of a wide range of research projects. The team develops analytical pipelines, joint genomics resources, training programs, data policies, and handles data management.

The team’s mission is to:
- Establish and maintain high throughput computational pipelines.
- Collaborate and support NYUAD’s multidisciplinary research programs.
- Provide Scientific project management solutions to researchers.
- Establish and maintain data management solutions.
- Provide expert scientific consultation and advice.
- Bioinformatics training and personal development to the wider NYUAD community.
- Develop new tools and resources for the analysis, visualization and management of high throughput genomics datasets.

The team focuses on the following types of analysis:
- Resequencing and structural variation analysis.
- De novo genome and transcriptome assembly.
- Metagenomic (amplicon and shotgun) assembly and analysis.
- Epigenetic analysis.
- Gene finding and annotation.
- Expression analysis (differential gene expression and transcriptome profiling) on whole and Single Cell RNAseq.
- Integrative genomics analysis (scRNA, scATAC, Proteome, Metabolome).
- ML/DL analysis modelling.

Our team includes individuals with diverse backgrounds and experiences, which enables us to target the focus areas mentioned above.

- Kristin C Gunsalus - Director of Bioinformatics CGSB.
- Nizar Drou - Bioinformatics Lead Developer CGSB.
- Muhammad Arshad - Bioinformatics Data Analyst CGSB.
- Jayaram Radhakrishnan - Bioinformatics Infrastructure Engineer CGSB.
- Guiseppe Antonio Saldi - Data Computational Scientis.
- Nabil Rahiman - Bioinformatics Full Stack Developer CGSB.

To get in touch with us, please send us an email at nyuad.cgsb.cb@nyu.edu


## MISO

Our LIMS is based on the open source MISO software https://github.com/miso-lims/miso-lims.
If you are interested in submitting samples for sequencing at NYUAD, you will have to have the relevant information added in MISO.

You will first need to open an account on our MISO instance, and you can do that by filling out this [form](https://docs.google.com/forms/d/e/1FAIpQLSfx3CxLrFb7FRh0hZlUfy2V-n85u1OTxSKngCoCzqyEs9psNQ/viewform).

Our MISO instance can be accessed here https://miso.abudhabi.nyu.edu/.

We have also added a [quick video](https://youtu.be/vE5mFv-zMpk) MISO tutorial.

Once you have opened your account successfully, you will be able to start submitting samples for sequencing, and if you face any issues, then please let us know using the email address nyuad.cgsb.cb@nyu.edu.


## GURU

[GURU](https://github.com/NYUAD-Core-Bioinformatics/guru) stands for **G**enomics seq**U**encing **R**un a**U**tomation, and it is an in-house developed software, which automates our sequencing data processing, data migration and archiving, as well the submission of workflows on the HPC.

Although GURU is currently accessible to a handful of people (mainly the Core Bioinformatics and Core Sequencing teams), we will be rolling it out to everyone very soon.

So why do we need such a system?

Managing and maintaining a genomics infrastructure requires a multi-layered approach. Typically, that involves a Laboratory Information Management System (LIMS), the 
Sequencing Instrumentation, the computational Infrastructure to store and process the data, as well as any other additional layers such as project management software (e.g. JIRA).
In a production environment, all of these layers need to efficiently communicate and integrate with each other, which can be a complicated task. In addition, the approach needs 
to be descriptive and yet flexible enough to accommodate new additions to the existing layers. Our solution, GURU (Genomics seqUencing Run aUtomation) addresses this need. GURU 
is implemented using Apache Airflow that allows for the authoring, scheduling and monitoring of workflows, or DAGs (Directed Acyclic Graph). Specific DAGs have been implemented 
to handle various sequencing runs, from SingleCell applications, to RNA/DNA sequencing, Short reads vs Long reads, archiving of sequencing runs, initiating specific types of 
analysis (QC/WGS/WES/RNAseq/ATAC/CHiP etc.), as well as automatically communicate to end-users regarding the status of their samples/runs.
GURU has been containerized using Docker to enable easy deployment across various configurations.

In our current implementation, GURU is at the heart of our sequencing data processing. The steps below summerize how the system works in its current format:

1. Once a sequencing run is complete, GURU will send an email notification to the Core Bioinformatics team, the Core Sequencing team, as well as this people who submitted the sequnced samples (owners). The email contains some basic information with regards to the run and it informs everyone that the run has started processing.
3. It then initiates the data transfer from the sequencing directory to the working directory on the HPC cluster.
4. It connects to the MISO LIMS system to generate the samplesheet for the run and performs some precheck validation on the CSV generated samplesheet, including validating the sample name format, replacing special character symbols, and applying correct adapter sequences, etc.
5. It proceeds with demultiplexing the run using bcl2fastq.
6. Once demultiplexing is complete, it proceeds to run the QC/QT (Quality Checking and Quality Trimming) WF using Biosails.
7. Once QC/QT is complete, GURU will sync the whole run to our archive storage without deleting it from the $SCRATCH working directory.
8. Finally, GURU will send out another email to the same users in step 1, infroming them wether the run processing has completed successfully or not, and attaching a MultiQC quality report to that email.

The current iteration of GURU will see it transform into a complete stand-alone system that will allow users to select and customize their analysis using a friendly user interface. Once the run processing is complete, users will get an email with a link that they can follow, and select from existing workflows, tag samples, modify workflows on the fly, and submit their analysis.

The system is very flexible an customizable, and it can be "plugged-in" to various workflows, even beyond genomics. If you are interested in using GURU for your research or setup, then please send us an email.


## JIRA

One of the first systems to be deployed by the Core Bioinformatics was a project management solution, [JIRA](https://www.atlassian.com/software/jira) back in 2014.

This might be counter-intuitive at first because you would think that we would be busy deploying software and writting analysis pipelines (or WFs), but if you don't document your work, then you would be lost after 10+ years of supporting various research programs!

We wanted a centralized location where we document all the development and analysis work that we carry out, including what analysis relates to which projects/samples/sequencing runs.

JIRA is a commercial software that has been used in a variety of settings, be it software development, advertisment, accounting, or even scientific project management. 

One thing to note is that our JIRA version is quite outdated, but this is not by choice. We wanted a system that we have full control over it, from the front-end as well as the backend database, and one that we can deploy locally on our servers, and authenticate using our existing NYU methods. The latest version doesn't allow for that unfortunately unless we purchase a very (VERY) expensive data warehouse license.

Still, even though we are working with an outdated version, the system still provides everything we need in terms of scientific project management.

The way JIRA integrates with our high throughput sequencing and analysis at the moment is as follows:

1. Once a sequencing run is complete, the core sequencing team creates a ticket under the NYUAD Core Sequencing (NCS) project in JIRA. This is a unique auto-incremental ID for a particular run (e.g. NCS-464, NCS-465 etc.). In this ticket, there is information regarding the person(s) who submitted the samples for sequencing, a brief description of the samples, and the name of the sequencing Flowcell.
2. GURU is then launched by the sequencing team members and this NCS ticket is provided during the execution of GURU.
3. GURU will then automatically find the ticket and send regular updates regarding the processing of the run (e.g. whether it is being demultiplexed, it is in QC/QT, full path to the run folder on the cluster etc.).
4. Once the run has finished processing in GURU, the ticket then gets assigned to a member of the Core Bioinformatics team for final review (to ensure nothing went wrong).
5. After the successful evaluation of the run, and if further downstream analysis is needed, a member of the Core Bioinformatics will create an analysis ticket under the NYUAD Core Bioinformatics (NCB) project in JIRA, and link it to the relevant NCS ticket. Additionally, if the analysis relates to any other tickets in JIRA (say it is part of a multirun projects), the links to these other tickets will be added.
6. During the course of the analysis, we try and document as much information as possible including folder paths, issues that we faced and how we resolved them, software that was used and their installation and loading sequences, links to papers and/or other resources that are relevant to the analysis etc.
7. Once we complete the analysis, the tickets are then closed or assigned to other team members for further analysis.

Doing all of this means that we never lose track of any projects and we have a whole wealth of local resources that we can use to refer to when we need to repeat any analysis. It also means that we can very easily and quickly find out exactly where the data and metadata that relates to any project that we worked on actually is.
Finally, it makes the whole process of offboarding and onboarding (in terms of data and data analysis) that much easier!


If you require an account on our local JIRA instance, then please email us and we will arrange a quick tutorial on how everything is organized in JIRA and how you can interact with the system.




## NASQAR
NASQAR stands for **N**ucleic **A**cid **S**e**Q**uence **A**nalysis **R**esource, and it is a front-end web-based platform for high throughput sequencing data analysis and visualization.

The original NASQAR paper is available [here](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-020-03577-4).

NASQAR offers a collection of custom and publicly available open-source web applications that make extensive use of a variety of R packages to provide interactive data analysis and visualization. It is not just a front-end to popular R packages, because we have spent considerable time and effort redeveloping a lot of these packages to fix bugs but more importantly, add additional functionalities.
What we tried to address with NASQAR is not just to accomodate researchers who are not familiar with the command line and R, we wanted to proved users the same flexibility and analytical power without the need to install packages or code functionalities themselves. We also wanted a platform that can be accessed publically, or deployed locally in the easiest way possible. You can either run NASQAR on your own server or laptop in a few very easy steps, or use the public instance.

Currently, we are working on NASQAR 2.0, and in this release we are working hard to deploy many (MANY) more apps and improve the aesthetics and the user interface. In the latest release, we are including apps for:
- RNAseq (Bulk and SingleCell).
- Sequencing data QC.
- Metagenomics.
- Epigenetics.
- Whole genome and exome analysis (DNA).

During the hands-on workshop, we will run a live demo of the latest DESEQ2 app in NASQAR 2.0, and if you want to know more about NASQAR 2.0 and how to use/deploy it for your research, then please email us and let us know.

NASQAR Github page: https://github.com/nasqar/NASQAR

NASQAR 2.0 Github page: https://github.com/NYUAD-Core-Bioinformatics/Nasqar2

NASQAR publication: https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-020-03577-4

NASQAR 2.0 web address: https://nasqar2.abudhabi.nyu.edu/

PLEASE NOTE THAT THE ORIGINAL NASQAR PUBLIC WEBSITE IS NOT LONGER AVAILABLE AND IF YOU WANT ACCESS TO IT, THEN PLEASE DEPLOY IT YOURSELF USING DOCKER AS DOCUMENTED IN THE GITHUB PAGE.


## BioSAILs

[BioSAILs](https://www.biorxiv.org/content/10.1101/509455v1) stands for **B**ioinformatics **S**tandardized **A**nalysis **I**nformation **L**ayers, and it represents our in-house developed workflow management (WF) system.

Think of WFs as a system that enables the automation and execution of a series of predefined tasks.
WF should be able to:

1. Capable of scaling and adapting as the tasks or the requirements change.
2. Can abstract the backend process from the user.
3. Uses an interface to define and execute the tasks.
4. Should also allow for monitoring and reporting of the executed workflows.
5. Ideally, should allow for an easy entry barrier to new and less experienced users.
6. Ideally, should be easily deployed on different architectures, and support multiple system setups.
7. Should provide detailed logging in order to restart analyses and enable reproducible research.

There are a lot of WMS currently available and choosing the right one can be a challenge, but you should definitely pick one!

At NYUAD, BioSAILs is the engine behind all of our production level analyses, and it enables us to support the diverse research needs at NYUAD. It is also developed in-house, which means that it integrates seamlessly with our current HPC setup.
At a high level, BioSAILs is made up of 2 commands that automate the execution of YAML based workflows, the **biox** command, and the **hpcrunner.pl** command.
The **biox** command is responsible for reading a pre-defined YAML workflow and creating an executable shell script.
The **hpcrunner.pl** command can then process the resulting shell script and submit on a workstation, HPC, or cloud infrastructure.

BioSAILs has a number of advantages, mainly that it relies on YAML plain text format to define a workflow, it is easy to install and deploy using conda, it has a extensible REST API for more advanced users to utilize, and the fact that multiple production level WFs have already been written by the Core Bioinformatics team (so you don't have to reinvent the wheel!).

Although this page is **NOT** intended to explore BioSAILs in detail, we will be showing you how easy it is to execute a workflow using BioSAILs.

If you want to install BioSAILs, you will have to install the [**biox**](https://bioconda.github.io/recipes/perl-biox-workflow-command/README.html?highlight=biox#package-Recipe%20&#x27;perl-biox-workflow-command&#x27;) and [**hpcrunner.pl**](https://bioconda.github.io/recipes/perl-hpc-runner-command/README.html?highlight=hpc%20runner#package-Recipe%20&#x27;perl-hpc-runner-command&#x27;) commands through conda/bioconda.

If you are running BioSAILs on the NYUAD HPC (Jubail), then it is already installed for you, so let's go ahead and submit a simple workflow.

1. Login to the HPC (if you don't know how to do that, have a look [here](https://github.com/nizardrou/Variant-Detection-and-Annotation-workshop?tab=readme-ov-file#setting-up-the-environment-and-copying-the-data)).
2. Change to your own personal $SCRATCH directory
   ```
   cd $SCRATCH
   ```
4. Either copy the test folder or download the zipped folder [**biosails_test.zip**](https://github.com/nizardrou/Core_Bio_resources/blob/main/biosails_test.zip) that is included in this repo, and "cd" into that directory.
   ```
   cp -r /scratch/gencore/nd48/biosails_test . && cd biosails_test.sh
   ```
5. Load the BioSAILs software module
   ```
   module purge
   module load gencore
   module load gencore_biosails
   ```
6. We will now submit a workflow that runs FastQC on a number of FASTQ files, so let's first run biox,
   ```
   biox run -w fastqc_dalma.yml -o qc.sh
   ```
7. This creates a qc.sh shell script that we will be supplying to **hpcrunner.pl** to submit the job,
   ```
   hpcrunner.pl submit_jobs -i qc.sh
   ```
8. You can check the progress of the jobs by typing "**squeue**".

Once the jobs complete, the output will be in the following directory,
```
ls data/processed
```
In the folder, there is another YAML workflow, which aligns the FASTQ paired end reads vs the E. coli reference genome. The alignment uses BWA MEM, followed by SAMtools to post process the alignments.
You can run that workflow in a similar way to the example above.

```
biox run -w bwa-samtools-dalma.yml -o align.sh
hpcrunner.pl submit_jobs -i align.sh --project align
```

The output will be in the data/analysis directory.

To find what other WFs are available, have a look at the following folder on the HPC,
```
/scratch/gencore/workflows/latest/
```


## The HPC GENCORE software modules

One of the main deliverables of the Core Bioinformartics team at NYUAD has always been to maintain a Bioinformatics Software Stack on the HPC. We were involved early on with the team behind [Bioconda](https://bioconda.github.io/) (to find out more and read the orginal Bioconda paper, please follow this [link](https://www.ncbi.nlm.nih.gov/pmc/articles/pmid/29967506/)).

Collectively, our software stack is called **gencore**, and it has gone through 2 iterations so far with 2 main differences between them.

We deploy software in either one of the following ways:

1. Install from conda if the software is already available.
2. Installation from source in case it is not available as a conda package.
3. Build a conda receipe of the package, publish it in the appropriate channel, and the install it locally.

Installing the software is only the first part of the process, for these software to be accessible by all users, we build them into modules using [easybuild](https://easybuild.io/) so that users can simply use the existing "module load" structure that is already available on the HPC.
If for whatever reason that is not possible, then we build a distinct conda environment and provide instructions on how to load that environment.

If you need any software installed on the HPC, or even if you need help setting up your own personal software, just let us know using the email address at the top of this page.

### GENCORE version 1
The very first iteration of the gencore modules included software that were grouped together into distinct groups encompassing various analysis disciplines such as rnaseq, de novo assembly, epigenetics etc.

Although this method provided the advantage of just using a single load command to load multiple peices of software (e.g. loading gencore_rnaseq loads bowtie2, hisat2, star, stringtie, htseq-count etc.), it provided a number of challenges as the software stacks grew.

The first was that we didn't have the ability to search the software modules directly, meaning that if you wanted to know whether a particular software existed or not, there was no way to look for it on the HPC.

The second was contineous integration. Everytime we added a peice of software to these modules, we had to test them for compatability, and whilst this is ok if you have only a handful of software, it ended up taking hours and sometimes days to rebuild the modules.

Accessing the gencore/1 modules and loading the gencore_rnaseq for example
```
module purge
module load gencore
module load gencore_rnaseq
```

### GENCORE version 2
The second (and current) method of deploying the gencore modules (gencore/2) saw us going back to having each peice of software as its own individual package. Although this addessed the two main challenges that gencore/1 presented, it meant that we could not longer have groups of software under distinct analysis domains. That's not to say that it is not possible to address this shortcoming, but we found out that it doesn't offer a big advantage either.

It also meant that we can have multiple versions of software always readily available and simple to deploy. To load samtools version 1.9 for example using the gencore/2 stack,
```
module purge
module load all
module load gencore/2
module load samtools/1.9
```

If you want to find out what software is available within the gencore/2 modules,
```
module purge
module load all
module load gencore/2
module avail
```
To search for a particular software (e.g. the de novo assembler abyss)
```
module purge
module load all
module load gencore/2
module search abyss
```




This repo is intended to familiarize you with some of the Bioinformatics resources that are available to you at NYUAD. There is a lot more that we can describe and cover, but we feel that what we have described in this page should help you get up and running with your current projects, and as always, if we missed something, or if you have any suggestions, then just let us know at nyuad.cgsb.cb@nyu.edu.























