# Registering Samples

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <iframe src="https://www.youtube.com/embed/ChCsqoq-r-Y" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
</div><br/>

- [ERC000033 metadata checklist](https://www.ebi.ac.uk/ena/browser/view/ERC000033)
- [INSDC missing value reporting](https://ena-docs.readthedocs.io/en/latest/submit/samples/missing-values.html?highlight=insdc%20missing#reporting-missing-values)


## Interactive

For this, we will use the materials in the `samples/interactive/` folder of the example data. Here, we have the same spreadsheet in 2 different formats : 
- `sample_spreadsheet.xlsx` : this is in Excel format and has been annotated with colour-coding to highlight important features
- `sample_spreadsheet.tsv` : tab-separated version of the above spreadsheet - this is the format accepted by Webin 

In both cases, each row represents a sample and each column represents a metadata field.

#### Video 

## Programmatic

In this section, we will use the materials in the `samples/programmatic` folder of the example data. Here, you will find several XML files. Navigate to the directory to see the file list:
```bash
cd $WORKSHOP 
cd samples/programmatic
ls 
```

- `samples.xml` : this contains the same set of samples as those submitted interactively in the previous section.
- `submission.xml` : this XML is the same as that used to submit your study. It defines the `<ADD/>` action to create new samples.
- `submission_modify.xml` : this submission XML defines the `<MODIFY/>` action, to allow us to update existing samples.

#### Samples XML 
The samples XML format allows us to define many samples inside a `<SAMPLE_SET>` tag. Each sample (enclosed in `<SAMPLE>` tags), contains:
- `<TITLE>` tags : defining the title of the sample
- `<SAMPLE_NAME>` tags : defining the taxonomic information
- `<DESCRIPTION>` tags : providing a description of what's been sampled and 
- many `<SAMPLE_ATTRIBUTE>` tags : defining all other metadata fields

```{note}
Sample aliases are defined within the `<SAMPLE>` tag, e.g. `<SAMPLE alias='this_alias'>`.
In the example data, the alias has been suffixed with the word 'programmatic'. This is to avoid clashes with the same samples 
that were submitted interactively in the previous section. Aliases must be unique.
```

#### Submit the samples
As we did with study registration, let's send the samples XML and submission XML (with the `<ADD/>` action) to our test service
using cURL to perform a submission:
```bash
curl -u username:password -F "SUBMISSION=@submission.xml" -F "SAMPLE=@samples.xml" "https://wwwdev.ebi.ac.uk/ena/submit/drop-box/submit/"
```

Again, you should receive a receipt XML with information about submission success and accession numbers. Note that this time, you will receive a `<SAMPLE>` tag for each submitted sample (in this case, 3). Please take note of each sample alias and accession as we will use these later to submit data files against.

For more general information on programmatic sample registration, please see [our documentation](https://ena-docs.readthedocs.io/en/latest/submit/samples/programmatic.html).

#### Modifying a sample
Sample metadata can be updated at a later date. This can be achieved by editing the sample XML file to update the relevant fields, and resubmitting with a submission XML containing the `<MODIFY/>` action in place of `<ADD/>`.

1. First, check your submitted sample in our browser using one of your accessions in the search box: [https://wwwdev.ebi.ac.uk/ena/browser/home](https://wwwdev.ebi.ac.uk/ena/browser/home)
2. Now, open the `samples.xml` file and update a metadata field of your choice. e.g. new collection date. Save the file.
3. This time, we will submit with the `submission_modify.xml`, which instructs the service to update an existing sample. The update uses the alias to detect existing samples, so it is important not to change the alias.
```bash
curl -u username:password -F "SUBMISSION=@submission_modify.xml" -F "SAMPLE=@samples.xml" "https://wwwdev.ebi.ac.uk/ena/submit/drop-box/submit/"
```

Check your sample on the browser again, and see that the metadata has been updated *** IS THIS INSTANT?? ***

```{warning}
Although sample metadata can be updated, these updates are not automatically propagated to the EMBL files of their sequences. This 
is due to computational constraints.

Updating samples will be reflected in the sample page in the ENA browser, the BioSamples record, and the [COVID-19 Data Portal](https://www.covid19dataportal.org/).

If it is very important for your EMBL files to be updated with new metadata, please contact our helpdesk at virus-dataflow@ebi.ac.uk and 
we will endeavour to assist you.
```

```{tip}
Now we have our samples registered to our project, it's time to add some data files. We'll start with [submitting raw read data](submit_reads.html).
```
