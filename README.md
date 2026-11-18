# IR: Inverted Matrix Workshop

**Conestoga College | PROG8245 Machine Learning Programming | Group 2**

Build and verify a search pipeline that loads a real corpus and supports
Boolean queries, exact token phrases, TF-IDF ranking, and evidence retrieval for
a RAG prompt.

## Team

| Team member | Student ID |
|---|---|
| [Member 1 full name] | [Member 1 student ID] |
| [Member 2 full name] | [Member 2 student ID] |
| [Member 3 full name] | [Member 3 student ID] |

Roster confirmation is pending. The previous README recorded four names and the
workshop specifies three members. Record confirmed names in the project and put
student IDs in the course submission PDF.

The baseline Git history attributes the starter notebook (a7268a7), workshop
implementation (5120752), and corpus snapshot (f505ca3) to UbaidUllah777.
Additional teammate contributions await evidence from their own commits.

[Shared Group 2 repository](https://github.com/UbaidUllah777/Lab---IR-Inverted-Matrix.git)

## Corpus and repository files

The original downloader saved the title and HTML summary from each of 20
[Python Software Foundation RSS entries](https://pyfound.blogspot.com/feeds/posts/default?alt=rss).
The unchanged snapshot is tracked in sample_docs/. Each filename maps to
a stable zero-based document ID. The notebook decodes HTML entities and indexes
visible text. A blanket redistribution license and the exact capture date are
unverified. Run against the committed files to reproduce the results, since the
live feed changes.

| Path | Purpose |
|---|---|
| IR_InvertedMatrix_Workshop.ipynb | Instructor sections, implementation, validation, and saved outputs |
| sample_docs/blog_1.txt through blog_20.txt | Original RSS snapshot |
| requirements.txt | Pinned direct notebook dependencies |
| Group_2_Submission.pdf | Course submission sheet and shared GitHub URL, pending roster confirmation |

The instructor download also contains TF-IDF.ipynb, TF-IDF.pdf,
Week10_IRBasics_Students.pptx, and Table of Contents.html.

## Run on Windows

Use Python 3.13. Run these PowerShell commands from the repository root. The
first command creates the environment for a fresh checkout.

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m pip check
.\.venv\Scripts\python.exe -c "import nbformat; from nbclient import NotebookClient; p='IR_InvertedMatrix_Workshop.ipynb'; b=nbformat.read(p, as_version=4); NotebookClient(b, timeout=120, kernel_name='python3').execute(); nbformat.validate(b); nbformat.write(b,p)"
```

In VS Code, select the project's .venv kernel and use **Restart Kernel and Run
All**. The notebook fetches the NLTK English stop-word list when it is missing
and stores the downloaded data in the ignored .nltk_data/ cache.

## Implementation and verified results

| Stage | Implementation and checks |
|---|---|
| Collection and tokenization | HTML cleanup, Unicode normalization, case folding, and token boundary checks. The cleaned snapshot has 20 distinct documents, 13,309 tokens, and 2,514 unique tokens before stop-word removal and stemming. |
| Linguistic pipeline | English stop-word filtering and Porter suffix rules. Before-and-after assertions cover running to run, developers to develop, and testing to test. |
| Boolean retrieval | Each term maps to sorted document IDs. Direct scans validate every posting and both Boolean operators. SOFTWARE AND grants returned 8 documents and SOFTWARE AND NOT grants returned 5. Absent-term and stop-word cases also passed. |
| Biword and positional indexes | Adjacent pairs map to document IDs. Phrase lookup joins consecutive token offsets. Token-window scans verified python software (11 documents, 19 occurrences), security developer (4, 9), python software foundation (11, 19), and foundation software python (0, 0). Checks cover stop-word adjacency, repeated and overlapping terms, empty input, and absent terms. |
| TF-IDF and ranking | For softwar, DF = 13 and IDF = ln(20/13) = 0.430783 to six decimals. Document 0 has TF = 2 and TF-IDF = 0.861566. The query Python software foundation grants ranked document 4 first at 5.1767. A direct calculation matched the ranking and scores. |
| RAG and agent | The agent retrieves scored excerpts and assembles a citation prompt. Tests compare source IDs and scores to ranked results, check excerpts against the original text, and exercise the insufficient-evidence branch. The run ends at prompt construction. |

The earlier count of **19,958 total tokens and 2,766 unique tokens** used a
lowercase word-character regex on raw RSS files, including HTML. The two
measurements use the same files. The cleaned result also uses different Unicode,
apostrophe, and underscore rules.

All 12 code cells ran in a fresh kernel with assertions enabled. A second
fresh-kernel run reproduced the saved outputs.

## Original team talking points

- Counting HTML tags and attributes can inflate corpus vocabulary.
- Keeping stop words in the positional stream prevents *python and software*
  from matching *python software*.
- A biword posting answers a two-token query directly. Positional joins verify
  that all words in a longer phrase align at the same start.
- A rare term can increase a score even when it is incidental to the question.
  The excerpts provide the evidence needed to check a proposed answer.
- Stable document IDs and score tie-breaking make repeated runs easier to compare.

## Submission checklist

- [ ] Confirm the roster and fill in the three names and IDs in the course PDF.
- [ ] Review the workshop together and record three genuine contributions by the
  actual team members on the shared repository.
- [ ] Send one instructor email with the .git URL and subject
  **PROG8245 - Inverted Matrix Workshop, Team #2**.
- [ ] Upload the finalized PDF to the course Dropbox.
- [ ] Request the official submit_assignment.py and the exact Group 2 identifier.
  The course ZIP lacks the script. The original command remains visible at the
  end of the notebook for the separate instructor GitHub step.
