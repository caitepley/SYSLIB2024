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


