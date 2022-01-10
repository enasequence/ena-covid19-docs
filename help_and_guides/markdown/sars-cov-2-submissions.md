# SARS-CoV-2 (Severe acute respiratory syndrome coronavirus 2) Submissions

Please see below for instructions on how to submit SARS-CoV-2 (Severe acute respiratory syndrome coronavirus 2) or COVID-19 related data. If you have any queries or require assistance with your submission please contact us at: virus-dataflow@ebi.ac.uk.

## Registering Studies
Data submissions to the ENA require that you register a study to contextualise and group your data. Details of how to do this can be found in our [Study Registration Guide](https://ena-docs.readthedocs.io/en/latest/submit/study.html). Please ensure you describe your study adequately, as well as provide an informative title.

Your ENA SARS-CoV-2 studies can now be claimed using your ORCID ID and/or assigned a DOI. Please see [here](https://ena-browser-docs.readthedocs.io/en/latest/about/citing-ena.html#orcid-data-claiming) and [here](https://ena-browser-docs.readthedocs.io/en/latest/help_and_guides/sars-cov-2-submissions.html#doi-issuing) for more information on these options.

## Registering Samples
Having registered a study, please proceed to register your samples. These are metadata objects that describe the source biological material of your experiments. Following this, the sequence data can be registered (as described in later sections).

Instructions for sample registration can be found in our [Sample Registration Guide](https://ena-docs.readthedocs.io/en/latest/submit/samples.html). As part of this process, you must select a sample checklist to describe metadata. If you require any support regarding sample metadata, please contact virus-dataflow@ebi.ac.uk.

### Viral Samples
The most appropriate checklist for SARS-CoV-2 viral submissions is the “ENA virus pathogen reporting standard checklist” - [ERC000033](https://www.ebi.ac.uk/ena/browser/view/ERC000033). This presents 9 mandatory, 15 recommended and 11 optional fields (along with any additional user-defined fields).

Please use the organism name `Severe acute respiratory syndrome coronavirus 2` and taxonomic ID 2697049. It is recommended, as a minimum, that collection date and geographic location (e.g. country) are specified and sample capture status field is provided a value of `active surveillance in response to outbreak`.
 
**Please see below for a template SARS-CoV-2 viral sample xml for programmatic submission to the ENA:**

```xml
 <SAMPLE_SET>
   <SAMPLE alias="Test SARS-CoV-2 sample 1" center_name="EBI">
    <TITLE>Test SARS-CoV-2 Sample 1 Title</TITLE>
    <SAMPLE_NAME>
      <TAXON_ID>2697049</TAXON_ID>
      <SCIENTIFIC_NAME>Severe acute respiratory syndrome coronavirus 2</SCIENTIFIC_NAME>
      <COMMON_NAME>SARS-CoV-2</COMMON_NAME>
    </SAMPLE_NAME>
    <SAMPLE_ATTRIBUTES>
      <SAMPLE_ATTRIBUTE>
        <TAG>geographic location (country and/or sea)</TAG>
        <VALUE>United Kingdom</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>collection date</TAG>
        <VALUE>2020-04-26</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>host common name</TAG>
        <VALUE>human</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>host subject id</TAG>
        <VALUE>1</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>host health state</TAG>
        <VALUE>diseased</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>host sex</TAG>
        <VALUE>female</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>host scientific name</TAG>
        <VALUE>homo sapien</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>collector name</TAG>
        <VALUE>Jane Smith</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>collecting institution</TAG>
        <VALUE>EMBL-EBI, Wellcome Genome Campus Cambridge CB10 1SD</VALUE>
      </SAMPLE_ATTRIBUTE> 
      <SAMPLE_ATTRIBUTE>
        <TAG>isolate</TAG>
        <VALUE>hCoV-19/UK/Bristol/2020</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>sample capture status</TAG>
        <VALUE>active surveillance in response to outbreak</VALUE>
      </SAMPLE_ATTRIBUTE>
      <SAMPLE_ATTRIBUTE>
        <TAG>ENA-CHECKLIST</TAG>
        <VALUE>ERC000033</VALUE>
      </SAMPLE_ATTRIBUTE>
    </SAMPLE_ATTRIBUTES>
   </SAMPLE>
 </SAMPLE_SET>
```

### Metagenomic Samples
Data submissions which include metagenomic samples, should be registered with a relevant metagenome taxonomy - visit our FAQ on [Tips for Taxonomy](https://ena-docs.readthedocs.io/en/latest/faq/taxonomy.html#environmental-biome-level-taxonomy) for more information. A few examples include human lung metagenome - [433733](https://www.ebi.ac.uk/ena/browser/view/Taxon:433733), human saliva metagenome - [1679718](https://www.ebi.ac.uk/ena/browser/view/Taxon:1679718), human tracheal metagenome - [1712573](https://www.ebi.ac.uk/ena/browser/view/Taxon:1712573) or human metagenome - [646099](https://www.ebi.ac.uk/ena/browser/view/Taxon:646099), among many others. Please contact us if you require help with this.

The most appropriate sample checklists depending on the source of your biological samples, are likely to include:

- GSC MIxS host associated ([ERC000013](https://www.ebi.ac.uk/ena/browser/view/ERC000013))
- GSC MIxS human associated ([ERC000014](https://www.ebi.ac.uk/ena/browser/view/ERC000014))

Visit our [ENA Sample Checklists](https://www.ebi.ac.uk/ena/browser/checklists) page for a full listing of sample checklists.

When using the GSC MIxS checklists for your submission, please include the optional field `host disease status` with a value of `COVID-19`.

### Other Sample Fields
If you have already submitted data to the GISAID database, a corresponding GISAID ID can be specified when using a sample checklist by creating a user-defined field named `GISAID Accession ID`.

## Submitting Reads
After registering your study and samples, you can submit your read files along with experimental (library-related) metadata. See our [Read Submission Guide](https://ena-docs.readthedocs.io/en/latest/submit/reads.html) for detailed instructions on submitting reads.

We encourage submissions to include information on specific protocols used for the experiment. This should be provided in the library description. This can be, for example, the name and/or URL to a specific protocol. View our listing of the available [full experimental metadata dictionaries](https://ena-docs.readthedocs.io/en/latest/submit/reads/webin-cli.html).

```{note}
Submitted reads to ENA should not contain human identifiable reads. Please filter out human reads prior to submission - if required, [here](https://github.com/alakob/Metagen-FastQC-Docker) is a tool which can be used.
```

## Submitting Assemblies
If submitting assemblies, you must have registered a study and a sample beforehand. It is also advised that the associated read data is also submitted. For instructions on assembly submission view our [Assembly Submission Guide](https://ena-docs.readthedocs.io/en/latest/submit/assembly.html).

Assemblies can only be submitted using [Webin-CLI program](https://ena-docs.readthedocs.io/en/latest/submit/general-guide/webin-cli.html) or [Webin SARS-CoV-2 Genome Submission Web API](https://ena-browser-docs.readthedocs.io/en/latest/help_and_guides/Webin-Cli_SARS-CoV-2_Genome_Submission_REST_API.html).

In case of [Webin-CLI program](https://ena-docs.readthedocs.io/en/latest/submit/general-guide/webin-cli.html) `-context genome` should be used.  During the process, you must define metadata in the [manifest file(s)](https://ena-docs.readthedocs.io/en/latest/submit/assembly/genome.html#manifest-files). Please specify ‘COVID-19 outbreak’ as the `ASSEMBLY_TYPE`.

```{tip}
The `COVERAGE` value should represent the mean depth of sequencing coverage across the submitted genome assembly. If unsure, we recommend calculating this from the total length of the genome assembly (`genome_len`), the number of reads (`num_reads`), and the average read length (`read_len`) as `(num_reads*read_len)/genome_len`.
```

```{tip}
The `MINGAPLENGTH` value controls the generation of `assembly_gap` features in EMBL and GenBank files (see [here](https://www.insdc.org/files/feature_table.html#7.2) for more information). Only gaps longer than, or equal to, the `MINGAPLENGTH` value will be listed in the file header. If unsure, please omit this value to fall back to our internal default value.
```

Any annotations, where provided, are captured according to [INSDC Feature Table Definitions](http://www.insdc.org/files/feature_table.html).

In alignment with INSDC partners, COVID-19 assemblies will **not** be assigned a GCA accession. However, sequence accessions will continue to be assigned, alongside ERZ analysis accessions which are the point of access for the submitted file(s). For more details on accessioning, view our [Accessions Guide](https://ena-docs.readthedocs.io/en/latest/submit/general-guide/accessions.html). To cite data, top-level project accessions (PRJ...) should be used as these are the most stable long-term accessions. View our [guide to cite data](https://ena-docs.readthedocs.io/en/latest/submit/general-guide/accessions.html#how-to-cite-your-ena-study) for further details.

## Submitting Targeted Sequences
If submitting targeted or annotated sequences, you must register a study as described above. See our [Targeted Sequence Submission Guide](https://ena-docs.readthedocs.io/en/latest/submit/sequence.html) for submission instructions. When submitting annotated sequences, you must select an appropriate [Annotation Checklist](https://ena-docs.readthedocs.io/en/latest/submit/sequence/annotation-checklists.html). There are several virus-specific annotation checklists, with “Single Viral CDS” the most appropriate for complete or partial coding sequences from a viral gene. If your sequences do not fit the annotation checklists above please contact us at virus-dataflow@ebi.ac.uk.

Any annotations, where provided, are captured according to [INSDC Feature Table Definitions](http://www.insdc.org/files/feature_table.html).

If submitting single contig assemblies, or for any other support or issues around SARS-CoV-2 submissions please contact virus-dataflow@ebi.ac.uk.

## Submitting Linked Human and Viral Datasets
For linked human and viral data submissions please contact virus-dataflow@ebi.ac.uk. Viral data should be submitted to ENA, with the corresponding human data being submitted to the [European Genome Phenome Archive (EGA)](https://www.ebi.ac.uk/ega/home). The viral and human samples registered during each submission will reference each other to support data discovery and interoperability. This requires registration of three types of samples:

1. Sample representing the human donor, registered at EGA.
2. Human sample, registered at EGA.
3. Viral sample, registered at ENA.

The sample representing the human donor (1) must be registered first as the human and viral samples (2 and 3) will reference this. Samples 2 and 3 do not need to be registered in order. To assist in linking data, the relevant BioSample accessions should be provided when contacting virus-dataflow@ebi.ac.uk.

## Release of Data
We recommend that submitted data is set to public as soon as possible to enable early presentation in [ENA](https://www.ebi.ac.uk/ena/browser/home) and also on the [COVID-19 data platform](https://www.covid19dataportal.org/). Users are responsible for releasing data they submit to ENA. This is done by setting an appropriate release date, as detailed in our [Data Release Policies](https://ena-docs.readthedocs.io/en/latest/faq/release.html#can-i-advance-postpone-the-release-date).

## DOI Issuing
We can now offer DOI issuing for SARS-CoV-2 projects. Digital Object Identifiers (DOIs) are persistent identifiers that can be assigned to any type of entity. From the [DOI handbook](https://www.doi.org/doi_handbook/1_Introduction.html#1.6.1):

> A DOI name is an identifier (not a location) of an entity on digital networks. It provides a system for persistent and actionable identification and interoperable exchange of managed information on digital networks. A DOI name can be assigned to any entity — physical, digital or abstract — primarily for sharing with an interested user community or managing as intellectual property. The DOI system is designed for interoperability; that is to use, or work with, existing identifier and metadata schemes. DOI names may also be expressed as URLs (URIs).

DOI issuing for ENA records is performed by creating a BioStudies record containing all relevant ENA projects ([https://www.ebi.ac.uk/biostudies/about](https://www.ebi.ac.uk/biostudies/about)). We will generate this BioStudies record on your behalf and it will hold pointers to the ENA project(s) of your choosing.

To request a DOI for your data, please email virus-dataflow@ebi.ac.uk.
