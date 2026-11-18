# IR — Inverted Matrix Workshop

Conestoga College · PROG8245 Machine Learning Programming · Group 2

This workshop builds an inverted index for Boolean retrieval, a biword and positional
index for phrase search, and a TF-IDF ranker that supplies cited excerpts for a
retrieval-augmented generation (RAG) prompt.

## Team

| Team member | Student ID |
|---|---|
| [Member 1 full name] | [Member 1 student ID] |
| [Member 2 full name] | [Member 2 student ID] |
| [Member 3 full name] | [Member 3 student ID] |

Repository: https://github.com/UbaidUllah777/Lab---IR-Inverted-Matrix.git

## Corpus and files

- The [Python Software Foundation blog RSS](https://pyfound.blogspot.com/feeds/posts/default?alt=rss) supplied the existing local files in sample_docs/. Each contains one title and HTML summary. The capture date and blanket redistribution license are unverified. Use a local copy of the same 20 files for exact reproduction. The live feed changes over time.
- IR_InvertedMatrix_Workshop.ipynb contains the workshop, assertion checks, and saved outputs.
- requirements.txt pins the direct notebook dependencies used in the verified run.
- Group_2_Submission.pdf contains the repository URL and team placeholders.
- The adjacent instructor download contains TF-IDF.ipynb, TF-IDF.pdf, Week10_IRBasics_Students.pptx, and Table of Contents.html. It has no submit_assignment.py.

## Run on Windows

From the repository root in PowerShell:

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -c "import nbformat; from nbclient import NotebookClient; p='IR_InvertedMatrix_Workshop.ipynb'; b=nbformat.read(p, as_version=4); NotebookClient(b, timeout=120, kernel_name='python3').execute(); nbformat.validate(b); nbformat.write(b,p)"
```

Alternatively, select the .venv kernel in VS Code and use **Restart Kernel and Run All**.
The notebook retrieves the NLTK English stop-word list if needed and caches it locally.

## Verified run

- 20 distinct documents, 13,309 tokens, and 2,514 unique tokens after HTML cleanup.
- SOFTWARE AND grants returned 8 documents. SOFTWARE AND NOT grants returned 5.
  Membership and absent-term handling matched direct scans.
- Positional results matched token-window scans for python software (11 documents,
  19 occurrences), security developer (4 documents, 9 occurrences), and a negative query. The biword postings and the stop-word adjacency regression passed.
- For software, DF = 13, IDF = 0.430783, and document 0 TF = 2 and TF-IDF = 0.861566.
  The ranked query returned document 4 first at 5.1767 and matched direct scoring.
- The agent prepared a prompt with validated source IDs and exercised the
  insufficient-evidence branch. Model generation is outside the demo.

## Team and submission checklist

- [ ] Confirm all three names and IDs for the PDF.
- [ ] Review the workshop as a team and have each member make a meaningful commit on the shared GitHub repository.
- [ ] Send one instructor email with subject PROG8245 - Inverted Matrix Workshop, Team #2.
- [ ] Submit the completed PDF through the course Dropbox.
- [ ] Obtain the official submission script and confirm the Group 2 identifier for the instructor's course GitHub step.
