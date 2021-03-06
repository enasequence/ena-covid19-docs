# Getting Started

## Introduction

In this workshop, we will begin by stepping through the available options to submit SARS-CoV-2 data to the [European Nucleotide Archive](https://www.ebi.ac.uk/ena/browser/home) using a series of example data and files we've prepared for you. For a complete submissions guide, please see [here](../help_and_guides/sars-cov-2-submissions).

The goal of this workshop is to submit 3 samples to an example project, along with raw read data and sequences associated with each sample. We will do this using a number of different submission options.

### Metadata Model Guide

Before submitting any data, it is important to understand the structure of our [metadata model](https://ena-docs.readthedocs.io/en/latest/submit/general-guide/metadata.html).
This model is used, not only for SARS-CoV-2 data, but data from across the tree of life. In this 
short video, I will touch on the importance of each element of the model and what data/metadata each
object holds.

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <iframe src="https://www.youtube.com/embed/M9srsSieEB4" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
</div><br/>

### Submission Routes

1. **programmatic**: most suitable for high-throughput, frequent submissions and automated systems
2. **interactive**: most suitable for infrequent submission, or those more comfortable with spreadsheets
3. **drag-and-drop uploader**: most suitable for once-off submission of small-to-meduim scale datasets

```{note}
We will use the test servers for this workshop. These service URLs begin with `wwwdev`
instead of `www`. Submissions to this service are removed nightly. 
```

### Workshop Setup

Before we begin, please download the example data [here](https://github.com/enasequence/ena-covid19-docs/raw/master/submission_workshop/example_data.tar.gz) and unzip it. For this tutorial, you will need:
- a means to view/edit spreadsheets in Microsoft Excel format and a text editor,
ideally something with syntax highlighting for XML formatted files.
- a command line utility with [cURL](https://curl.se/) installed.
- basic command line skills.
- a Webin account. If you don't already have one, please register [here](https://www.ebi.ac.uk/ena/submit/webin/accountInfo).
- an [installation of Webin-CLI](https://github.com/enasequence/webin-cli/tree/v4.1.0#readme), our command line interface for the submission of data files . This requires Java 1.8 or higher.

```{tip}
Now, let's get started with [registering a study](register_study).
```
