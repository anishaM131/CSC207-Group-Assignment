# CSC207-Group-Assignment

## Ideas:
### ANISHA:
Entities: Paper, SectionTag, SectionNote
External API: OpenAlex API (or CrossRef API) for use case 1 for searching real academic papers by title, keyword, or DOI

#### 1. Search & Import Paper (API)
User story: As a researcher writing a paper, I want to search for academic articles by title, keyword, or DOI using an external literature API and save relevant results into my personal library, so that I do not have to manually type out bibliographic details.
flow/details:
1. User enters a search query (title, keyword, or DOI) into the search bar.
2. System queries the external academic API (e.g., OpenAlex or CrossRef) and displays matching papers (title, authors, year, abstract).
3. User selects a paper and clicks Add to Library (or uses a manual-entry option if a paper is not indexed).
4. System creates a Paper entity, saves it to persistent storage, and confirms it has been added without duplicates.
##### 2. Tag & Annotate for Paper Sections
User Story: As a writer organizing my sources, I want to assign paper-section tags (such as Introduction, Related Work, Methods, or Discussion) and attach short notes or quotes to saved papers, so that I remember how and where I plan to cite each source in my draft.
flow/details:
1. User selects a saved paper from their library.
2. User selects one or more section tags (predefined or custom) and enters a section-specific note (for ex. "Use this statistic for paragraph 2 of the Intro").
3. System updates the Paper entity with the SectionTag and note, persists the changes, and updates the paper's displayed tags in the UI.
#### 3. Filter & Search Library by Section
User Story: As a writer drafting a specific section of my paper, I want to filter my saved library by section tag, author, publication year, or keywords in my notes, so that I can quickly view only the sources relevant to the section I am currently writing.
flow/details:
1. User selects one or more filter criteria (e.g., tag = Introduction, year >= 2020 or a keyword search).
2. System applies the selected filter rules to the saved library and returns the matching subset of papers.
3. User can clear or combine filters dynamically to switch focus between different sections of their paper.
#### 4. Generate Section Outline & Citations
User Story: As a researcher transitioning from reading to writing, I want to export a structured outline for a selected paper section (or my entire library) containing my notes and formatted citations (e.g., APA, IEEE, or BibTeX), so that I can directly integrate my organized literature into my manuscript.
details/flow:
1. User selects a target scope (for ex. Introduction section only, or all sections) and chooses a citation format (APA, IEEE, or BibTeX).
2. System groups the matching papers by section, formats each reference according to the chosen style, and attaches the user's section notes underneath each citation.
3. User previews the generated outline and exports it to a local .md or a .txt file.
