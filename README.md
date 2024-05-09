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

Although this page is **NOT** intended to go explore BioSAILs in detail, we will be showing you how easy it is to execute a workflow using BioSAILs.

If you want to install BioSAILs, you will have to install the [**biox**](https://bioconda.github.io/recipes/perl-biox-workflow-command/README.html?highlight=biox#package-Recipe%20&#x27;perl-biox-workflow-command&#x27;) and [**hpcrunner.pl**](https://bioconda.github.io/recipes/perl-hpc-runner-command/README.html?highlight=hpc%20runner#package-Recipe%20&#x27;perl-hpc-runner-command&#x27;) commands through conda/bioconda.

If you are running BioSAILs on the NYUAD HPC (Jubail), then it is already installed for you, so let's go ahead and submit a simple workflow.

1. Login to the HPC (if you don't know how to do that, have a look [here]())



## The HPC GENCORE software modules



## The HPC Front end Interface


## Data arechiving/dearchiving, sharing, and submission to public repositories


## Tips and Tricks

























