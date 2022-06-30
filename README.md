---
# replace uri to point to the name resource you'd like to align
# a url without scheme like https:// (e.g., ```url: foodorganisms.txt```) 
# is assumed to be a local file in working directory
datasets:
    - url: foodorganisms.txt
      type: text/csv
#   - url: https://example.org/data.tsv
#     type: text/tab-separated-values
    - url: https://serv.biokic.asu.edu/ecdysis/content/dwca/UCSB-IZC_DwC-A.zip
      type: application/dwca
#   - url: https://example.org/rss.xml
#     type: application/rss+xml
taxonomies:
    - id: col
      name: Catalogue of Life
    - id: gbif
      name: GBIF Backbone Taxonomy
    - id: itis
      name: Integrated Taxonomic Information System
    - id: ncbi
      name: NCBI Taxonomy
    - id: globi
      name: GloBI Taxon Graph
---

# Name Alignment

[![Name Alignment by Nomer](../../actions/workflows/align.yml/badge.svg)](../../actions/workflows/align.yml)

Aligning taxonomic names is a common task in biodiversity informatics. 

This template repository offers an automated method to align scientific names in csv/tsv files and darwin core archive with common taxonomic name lists like Catalogue of Life, NCBI Taxonomy, Integrated Taxonomic Information System (ITIS), and GBIF Backbone taxonomy.

To re-use:

1. create your own repository using this repository as a template
2. edit the README.md and add the urls / filenames to the resources you'd like to review. Note that only the following types are supported at time of writing (June 2022): ```text/csv```, ```text/tab-separated-values```, ```application/dwca```. 
3. for now only names in column "scientificName" (tsv/csv), and "http://rs.tdwg.org/dwc/terms/scientificName" (DwC-A) will be aligned 
4. commit the changes to github
5. inspect results of name alignment in "Github Actions" (e.g., [sample results](https://github.com/globalbioticinteractions/name-alignment-template/runs/5468413931?check_suite_focus=true#step:5:144))
)
6. download results from provided single-use https://file.io link  (e.g., look for ```Download the name alignment results with the single-use, and expiring, file.io link at: https://file.io/[something]``` in alignment report)
7. to re-create results, change your name list in github or select ["re-run jobs" in Github Actions](https://docs.github.com/en/actions/managing-workflow-runs/re-running-workflows-and-jobs).

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

## Provenance of DwC-A Names

The name context of names extracted from DwC-A are captured in a funny looking text:

```
line:zip:hash://sha256/fe63af46ed66abd253ee148e383fb51da6695ce3848d0bde39af18aa77d364fb!/occurrences.csv!/L10
```

extracted from a generated ```names-aligned.tsv```:

```
$ cat names-aligned.tsv | grep hash | grep occurrence | head -n1
line:zip:hash://sha256/fe63af46ed66abd253ee148e383fb51da6695ce3848d0bde39af18aa77d364fb!/occurrences.csv!/L10	Lasioglossum	SAME_AS	line:zip:hash://sha256/fe63af46ed66abd253ee148e383fb51da6695ce3848d0bde39af18aa77d364fb!/occurrences.csv!/L10	Lasioglossum								HAS_ACCEPTED_NAME	COL:5B4P	Lasioglossum	genus		Biota | Animalia | Arthropoda | Insecta | Hymenoptera | Apoidea | Halictidae | Halictinae | Halictini | Lasioglossum	COL:5T6MX | COL:N | COL:RT | COL:H6 | COL:HYM | COL:625GP | COL:625H4 | COL:JMV | COL:KV7 | COL:5B4P	unranked | kingdom | phylum | class | order | superfamily | family | subfamily | tribe | genus	https://www.catalogueoflife.org/data/taxon/5B4P	
```

This text identifies the row from which the name was extracted. In this case, line 10, from file ```occurrences.csv``` contained in the zip file with content id ```hash://sha256/fe63af46ed66abd253ee148e383fb51da6695ce3848d0bde39af18aa77d364fb``` . If you retain the tracked dataset (in this case UC Santa Barbara Invertebrate Zoology Collection accessed on 2022-06-30) provided in the data/ folder of the name aligment archive,  you can use [Preston](https://preston.guoda.bio) to dig up the original record using:

```
$ preston cat 'line:zip:hash://sha256/fe63af46ed66abd253ee148e383fb51da6695ce3848d0bde39af18aa77d364fb!/occurrences.csv!/L10' 
881449,UCSB,IZC,,b03a3f0c-bfa5-4e02-b5d3-56ff38626302,PreservedSpecimen,a8a4f8b1-38f1-4e10-9b75-b2e86ac196fc,UCSB-IZC00038312,,Animalia|Arthropoda|Hexapoda|Insecta|Pterygota|Neoptera|Hymenoptera|Apocrita|Aculeata|Apoidea|Halictidae|Halictinae|Halictini,Animalia,Arthropoda,Insecta,Hymenoptera,Halictidae,Lasioglossum,186125,"Curtis, 1833",Lasioglossum,,,,,Genus,"EEMB/ENV S 96",24-May-2022,,,,,,"Sophie Cameron",,2022-04-26,2022,4,26,116,,,,"Newly restored salt marsh",PAN2,,,,,,,"on flower of Eschscholzia californica",,,Adult,Female,1,Pinned,"United States",California,"Santa Barbara",,"University of California Santa Barbara North Campus Open Space",,34.42174,-119.87186,WGS84,10,,,,GPS,,,,,,,,,,,,"2022-05-31 10:52:55",http://creativecommons.org/publicdomain/zero/1.0/,"The Regents of the University of California",https://www.ccber.ucsb.edu/collections/databases-searching-specimen-data-and-images,urn:uuid:a8a4f8b1-38f1-4e10-9b75-b2e86ac196fc,https://serv.biokic.asu.edu/ecdysis/collections/individual/index.php?occid=881449
```

which links to a preserved specimen with occurrenceId b03a3f0c-bfa5-4e02-b5d3-56ff38626302 and landing page at https://serv.biokic.asu.edu/ecdysis/collections/individual/index.php?occid=881449 . Also see [screenshot made on 2022-06-30](./img/UCSB-IZC00038312_b03a3f0c-bfa5-4e02-b5d3-56ff38626302.png). 

With this context, you can trace the origin and context of the name in great detail. This detail can be used to troubleshoot bugs in the name alignment process, or provide granular feedback to those that maintain the dataset or taxonomy.  



