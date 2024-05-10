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
- The HPC front-end interface.
- Customizing your submissions on the HPC including tips and tricks on how to get the best performance out of your analysis.



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

1. Once a sequencing runs is complete.
2. 

The system is very flexible an customizaqble, and it can be "plugged-in" to various workflows, even beyond genomics. If you are interested in using GURU for your research or setup, then please send us an email.


## JIRA



## NASQAR



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



## The HPC Front end Interface


## Data archiving/dearchiving, sharing, and submission to public repositories


## Tips and Tricks

























