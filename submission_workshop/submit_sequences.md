# Submitting Sequences

Submission of genomes/consensus sequences can only be achieved through Webin-CLI.

## Webin-CLI

As with read submission, submission of sequences through the Webin-CLI utility requires manifest files providing information about the data files. Using the `-context genome` we usually provide metadata about how the sequence was generated and from which platforms the underlying data originated. 

In the `sequences/webin-cli` directory, we provide all example files required to submit sequences against our 3 samples.
```bash
cd $WORKSHOP/sequences/webin-cli
ls
```

For each of our 3 samples, you will find:
1. a `*_manifest.txt` file defining information about the sequence, including the name of the fasta file containing the sequence 
2. a `*.fasta.gz` file : a fasta file containing the sequence data. This file must be compressed for submission
3. a `*_chrm_list.txt.gz` file : defining the list of 'chromosomes'. In the case of SARS-CoV-2, we simply list the sequences as 'chromosome 1' . This file must also be compressed

Each of the manifest files will need to be edited to add your own accessions in order to link these sequences to your existing objects. The following lines should be customised:
```
STUDY   PRJEB#####
SAMPLE  ERS#######
RUN_REF ERR#######
```

```{note}
Where possible, we recommend including a `RUN_REF` to link the sequence back to the raw read data it was built from.
```

As we did with reads, we will first validate our submission using the `-validate` flag.

```bash
java -jar webin-cli-4.2.0.jar -context genome -manifest hCoV-19_isolate_1_manifest.txt -userName user -password pass -test -validate
```

If this passes validation, we can replace the `-validate` flag with `-submit` to perform the submission.

```{warning}
Please use the `-test` flag to submit to our test service
```

```bash
java -jar webin-cli-4.2.0.jar -context genome -manifest hCoV-19_isolate_1_manifest.txt -userName user -password pass -test -submit
```

## Webin-CLI-REST

A new JSON-based REST service was introduced this year specifically for the submission of SARS-CoV-2 sequences. In this service, sequences are not held in fasta files - rather, they are included directly in the JSON payload itself, greatly simplifying the process of submission. This is only possible due to the small size and relatively low complexity of the genome. For more information on this system, including useful code snippets, please see our [documentation here](../help_and_guides/webin-cli-rest.html).

<!-- :::{tabbed} Unix/MacOS -->
```bash
cd $WORKSHOP/sequences/webin-cli-rest/
ls
cat hCoV-19_isolate_1.json
```
<!-- :::

:::{tabbed} Windows
```
cd $WORKSHOP\sequences\webin-cli-rest\
dir
```
::: -->

Note that this JSON object contains the exact same information as that of its equivalent manifest file. The only difference is that the sequence is embedded directly into the JSON payload. We will send the entire JSON object via the `POST` protocol to our Webin-CLI-REST (test) service using cURL.

This service also provides both validation and submission services, as with the Webin-CLI tool, but here we  `POST` to different URLs for each service:
- validation: [https://wwwdev.ebi.ac.uk/ena/submit/webin-cli/api/v1/genome/covid-19/validate](https://wwwdev.ebi.ac.uk/ena/submit/webin-cli/api/v1/genome/covid-19/validate)
- submission: [https://wwwdev.ebi.ac.uk/ena/submit/webin-cli/api/v1/genome/covid-19](https://wwwdev.ebi.ac.uk/ena/submit/webin-cli/api/v1/genome/covid-19/validate)

Let's validate the contents of `hCoV-19_isolate_1.json`. Remember to replace `-u user:pass` with your webin credentials, and to substitute in your own accessions into the JSON object:
```bash
curl -X 'POST' -u user:pass   \
  'https://wwwdev.ebi.ac.uk/ena/submit/webin-cli/api/v1/genome/covid-19/validate' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "study": "PRJEB#####",
    "sample": "ERS#######",
    "runRef": "ERR#######",
    "name": "hCov-19_isolate_1",
    "coverage": 100,
    "program": "ARTIC fieldbioinformatics (minimap2/nanopolish) 1.1.3 (nanopolish 0.13.2)",
    "platform": "OXFORD_NANOPORE",
    "minGapLength": 3,
    "moleculeType": "genomic RNA",
    "description": "example sequence #1 for workshop",
    "sequence": "NNNNNNNNNTTATACCTTCCCAGGTAACAAACCAACCAACTTTCGATCTCTTGTAGATCTGTTCTCTAAACGAACTTTAAAATCTGTGTGGCTGTCACTCGGCTGCATGCTTAGTGCACTCACGCAGTATAATTAATAACTAATTACTGTCGTTGACAGGACACGAGTAACTCGTCTATCTTCTGCAGGCTGCTTACGGTTTCGTCCGTGTTGCAGCCGATCATCAGCACATCTAGGTTTTGTCCGGGTGTGACCGAAAGGTAAGATGGAGAGCCTTGTCCCTGGTTTCAACGAGAAAACACACGTCCAACTCAGTTTGCCTGTTTTACAGGTTCGCGACGTGCTCGTACGTGGCTTTGGAGACTCCGTGGAGGAGGTCTTATCAGAGGCACGTCAACATCTTAAAGATGGCACTTGTGGCTTAGTAGAAGTTGAAAAAGGCGTTTTGCCTCAACTTGAACAGCCCTATGTGTTCATCAAACGTTCGGATGCTCGACTGCACCTCATGGTCATGTTATGGTTGAGCTGGTAGCAGAACTCGAAGGCATTCAGTACGGTCGTAGTGGTGAGACACTTGGTGTCCTTGTCCCTCATGTGGGCGAAATACCAGTGGCTTACCGCAAGGTTCTTCTTCGTAAGAACGGTAATAAAGGAGCTGGTGGCCATAGTTACGGCGCCGATCTAAAGTCATTTGACTTAGGCGACGAGCTTGG"
  }'
```

To submit the sequence, simply remove `/validate` from the URL above and run again.
