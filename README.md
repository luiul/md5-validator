# MD5 Validator

Notebook to validate submitted PDF files against submitted md5 checksums. Student ID must be checked manually by a tutor.  

## Workflow

This section offers an overview of the two stages of the workflow.

The first stage of this notebook takes as input I1:

- raw HTML files with submitted md5 from students
- raw PDF files submitted by students (contains duplicates)
- csv file with student information (Matrikel, Name, Mail, SS (Startsemester), PO (Prüfungsordnung))

In the first stage, we generate the following output s(I1)=O1:

- data frame and CSV file with md5 of PDF files
- data frame file with submitted md5 from students
- data frame and CSV file with valid submissions
- data frame and CSV file with invalid submissions

In the first stage, we also rename the PDF files according to the valid submissions data frame. After the first stage, the valid PDF files are graded and stored in the `./korrigiert` directory.

The second stage takes as input I2:

- graded PDF files

In the second stage, we generate the following output s(I2)=O2:

- encrypted graded PDF files

After the graded PDF files are encrypted, they are ready to be uploaded publicly. For administrative purposes, the encrypted files have an owner key that can open all files.

## Stages in Detail

This section describes the two stages of the notebook in detail.

### Stage 1

In this stage we:

- generate MD5 from uploaded PDF files & delete duplicates
- store MD5 from PDF files as data frame A
- scrape MD5 from HTML files
- extract name from HTML files
- store scraped MD5 and extracted names as data frame B
- inner join A and B to determine valid submissions; store the resulting data frame C
- read student ID data and store it as data frame D
- inner join C and D to get additional information for the valid submissions; store the resulting data frame E

Don't forget to normalize strings and remove white spaces!

### Stage 2

In this stage we:

- encrypt the graded PDF files against the data frame with valid submissions

Rerun the whole notebook before Stage 2, to store the data frame with valid submissions in memory
