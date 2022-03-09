# Name Alignment

[![Name Alignment by Nomer](https://github.com/globalbioticinteractions/name-alignment-template/actions/workflows/align.yml/badge.svg)](https://github.com/globalbioticinteractions/name-alignment-template/actions/workflows/align.yml)

Aligning taxonomic names is a common task in biodiversity informatics. 

This template repository offers an automated method to align any text file with names against common taxonomic name lists like Catalogue of Life, NCBI Taxonomy, Integrated Taxonomic Information System (ITIS), and GBIF Backbone taxonomy.

To re-use:

1. create your own repository using this repository as a template
2. edit the README.md and replace line 3 reference of ```globalbioticinteractions/name-alignment-template``` to your own github repo (e.g., ```dduck/mynames``` with ```[github user/org]/[repository name]```) 
3. add/replace your own name table in a file with .txt/.tsv (for tab-separated files) and .csv (for semi-colon seperated files) extension
4. only name in column "scientificName" will be aligned 
5. commit the changes to github
6. inspect results of name alignment in "Github Actions" (e.g., [sample results](https://github.com/globalbioticinteractions/name-alignment-template/runs/5468413931?check_suite_focus=true#step:5:144))
)
7. download results from provided single-use https://file.io link  (e.g., look for ```Download the name alignment results with the single-use, and expiring, file.io link at: https://file.io/[something]``` in alignment report)
8. to re-create results, change your name list in github or select ["re-run jobs" in Github Actions](https://docs.github.com/en/actions/managing-workflow-runs/re-running-workflows-and-jobs).



# Origin

This repository was conceived on 2022-03-08 during the [Alien CSI Hack-a-thon](https://github.com/alien-csi/alien-csi-hackathon) in Romania by Christina, Quentin, Jorrit, Jasmijn, .... For more information see https://github.com/alien-csi/alien-csi-hackathon . 

# Contributors


name | affiliation | orcid 
--- | --- | ---
Jorrit Poelen | GloBI; Ronin Institute | https://orcid.org/0000-0003-3138-4118
your name | your affiliation | your orcid


# Feedback / issues

This repository uses scripts in https://github.com/globalbioticinteractions/globinizer. These script use commandline tools like [GloBI](https://globalbioticinteractions.org)'s [nomer](https://github.com/globalbioticinteractions/nomer), cut, sed, etc. 

# Misc Notes


install nomer java8 / java11 - 

https://github.com/globalbioticinteractions/nomer 

e.g., Carl Boettiger taxondb R package


Print names and add a tab in front, to prepare for nomer. 

```
cat foodorganisms.txt | sed 's/^/\t/g' > foodorganisms.tsv
```

Nomer expects the format to be:

[id][tab][name]

e.g.,
id\tname
NCBI:9606\tHomo sapiens


Print names to screen and append itis taxonomic interpretation, and write/redirect to a file 'name-itis.tsv'

```
cat foodorganisms.tsv | nomer append itis > name-itis.tsv
```

open in LibreOffice Calc

Repeat with 'gbif' instead of 'itis'






