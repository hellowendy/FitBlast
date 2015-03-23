# FitBlast
A website to easily retrieve and display fitness data from SQL database

## File description

# myFrontPage.cgi
The entering page to run FitBlast
Options for searching:
1. GENE -> myFitShow.cgi
- locusId (need to be exact match)
- sysName (need to be exact match)
- specific species + locusId/sysName
- "All 17 genomes" + gene name (case insensitive)
- specific species + gene name (case insensitive)
Note: if more then one hits were found, a table listing all hits with links to fitness data will be shown.
2. SEQUENCE -> mySeqSearch.cgi
nucleotide
protein (default)

# mySeqSearch.cgi
This page shows blast result when:
1. doing sequence search from the front page
- will save the input sequence, run blast, parse and show top blast hits
- if fitness data is available for a gene, a link will be provided -> myFitShow.cgi
2. asking for homologs from the fitness page
- the gene will be specified by the "species" name and "locusId" submitting from myFitShow.cgi
- will extract gene sequence, run blast, parse and show top blast hits
has link to the front page -> myFrontPage.cgi

# myFitShow.cgi
Function:
- 1. show fitness
- 2. link to homologs -> mySeqSearch.cgi
has link to the front page -> myFrontPage.cgi
This page shows fitness when:
1. check fitness from blast page
2. centain gene is specified from the front page
3. direct url with gene specified
Parameters:
- species: optional
- gene: must be specified, locusId or sysName or gene name
- when the scenario satisfies i) species is not specified AND ii) gene name or locusId is given iii) the matched genes are more than one, a table of corresponding genes will be shown, notifying if fitness data is available for each gene
Fitness heatmap color scheme:
blue(-3)-white(0)-yellow(+3)

# Database:
Database schema:
Organism Table
- orgId  nickname(primary key)  genus  species  NCBI_taxonomyId
Gene Table
- orgId nickname locusId sysName type    scaffoldId      begin   end     strand  name    desc    GC      nTA
- PRIMARY KEY (nickname, locusId)
Experiment Table
- orgId expId Group short_description media vessel temperature pH Condition_1 Concentration_1 Units_1
- PRIMARY KEY (nickname, expName)
GeneFitness Table
- species locusId expName fit t
- PRIMARY KEY (species,locusId,expName)

## END

