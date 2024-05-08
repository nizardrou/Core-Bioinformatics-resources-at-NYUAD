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


























