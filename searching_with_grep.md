Task: Create a new file in your GitHub repository. Use markdown formatting to write a page of example grep queries and notes as you examine your Scopus data. Be sure to post more than your queries. 
Write about the data, what each grep command that you create seeks to do, etc. That is, be descriptive and document your process, queries, intentions, etc. Post a link here to your GitHub repo, and 
discuss or raise any questions you have in our Element. If you're having problems with Element, let me know. It's required that you participate
there this week.

# Searching with grep

## Uploading Data
I could not get the scopus.bib file transferred using the command from the text/lecture, so I used the alternative method instead. I exported the data that I wanted from Scopus, added it to this git repo (under scopus.bib), 
and then used `wget` with the URL of the data on github. This worked great. 

Once I was done following along with the example from the lecture, I wanted to explore other articles from Scopus. I used the search term `"galaxy clusters" AND python` to return documents related to both galaxy clusters and python programming. There were 28 results, so I exported all of the citation and bibliographic information into the file named scopus_galaxy.bib. I then uploaded the file to my VM using the `wget` command again.

## Example data from `scopus_galaxy.bib`
@ARTICLE{Tortorelli2023,
	author = {Tortorelli, Luca and Mercurio, Amata},
	title = {MORPHOFIT: An automated galaxy structural parameters fitting package},
	year = {2023},
	journal = {Frontiers in Astronomy and Space Sciences},
	volume = {10},
	doi = {10.3389/fspas.2023.989443},
	url = {https://www.scopus.com/inward/record.uri?eid=2-s2.0-85150702781&doi=10.3389%2ffspas.2023.989443&partnerID=40&md5=5f77456285a8fc60432e53977278bc7e},
	affiliations = {Faculty of Physics, University Observatory, Ludwig-Maximilians-Universität München, Munich, Germany; Institute for Particle Physics and Astrophysics, ETH Zürich, Zürich, Switzerland; Dipartimento di Fisica “E.R. Caianiello“, Università degli Studi di Salerno, SA, Fisciano, Italy; INAF- Osservatorio Astronomico di Capodimonte, Napoli, Italy},
	correspondence_address = {L. Tortorelli; Faculty of Physics, University Observatory, Ludwig-Maximilians-Universität München, Munich, Germany; email: Luca.Tortorelli@physik.lmu.de},
	publisher = {Frontiers Media S.A.},
	issn = {2296987X},
	language = {English},
	abbrev_source_title = {Front. Astron. Space Sci.},
	type = {Article},
	publication_stage = {Final},
	source = {Scopus},
	note = {Cited by: 0; All Open Access, Gold Open Access, Green Open Access}
}

This file contains the metadata for the publications that the search query returned.
## grep Commands
### Document Types
I wanted to see what kinds of documents were returned to create the file that we are looking at here. I used the command `grep "^@" scopus_galaxy.bib`. This returned only the type Article, so that means that all of the documents in scopus_galaxy.bib are journal articles.

### Article Titles
Something I wanted to do was extract all of the titles from the `scopus_galaxy.bib`, so I used the command `grep "title = " scopus_galaxy.bib`. It returned this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/b420e635-cd0c-413d-86b1-845811c75192)
This is not really what I want because I just wanted to return the title, not the abbrev_source_title, so the command is going to need to be more specific. I tried the command `grep -P  "\ttitle = " scopus_galaxy.bib` and it produced this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/986e79f8-6695-4561-82a0-b7524d594638)
This is just the titles, which is what I wanted.

## Year Published
The next thing I wanted to do was find a count of the years that the articles in the file were published. This could be interesting to see how far back research on galaxy clusters using Python goes. I was hopeful that this line would work, `grep -Eio "year =[0-9]*" scopus_galaxy.bib | sort | uniq -c` , but it returned this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/4a63c09c-a219-46d8-9e0f-7d612ee7cc79)

This command just returned the count of articles that had a year associated with them (which was all of them)

The (very poor) solution that I came up with was to search for individual years, which looks like this:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/ec809bf8-6d2f-45f8-a884-b0188533fc24)

This returns the number of documents published in a particular year (in this instance, I chose 2013). I have yet to figure out how to return a count of the publications by year for the whole dataset.

### Total Citations
Another thing I wanted to look at was the total citations. We did this for the example in the lecture, but I thought it would be interesting to apply to the galaxy data to see how popular the research being published is. This is the command I used: `grep -o "Cited by: [0-9]*" scopus_galaxy.bib | \
    awk -F":" \
    'BEGIN { printf "Total Citations: "} \
    { sum += $2; } \
    END { print sum }'
`
This is what was returned:
![image](https://github.com/caitepley/SYSLIB2024/assets/148588703/e13be4fb-72d1-46c4-8b9c-06d3780970b3)

There were 302 citations for this dataset, which only had 28 documents, so I would say that the research being published on galaxy clusters using Python is decently popular. 





