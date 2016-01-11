#OCLC Entity Pilot Testing

##Sample Data

###[Ecommons](https://ecommons.cornell.edu)

OAI-DC Overview:

```
{http://purl.org/dc/elements/1.1/}contributor: |                         |    681/27821 |   2%
    {http://purl.org/dc/elements/1.1/}creator: |===================      |  21842/27821 |  78%
       {http://purl.org/dc/elements/1.1/}date: |=========================|  27821/27821 | 100%
{http://purl.org/dc/elements/1.1/}description: |======================   |  25203/27821 |  90%
     {http://purl.org/dc/elements/1.1/}format: |======                   |   7779/27821 |  27%
 {http://purl.org/dc/elements/1.1/}identifier: |======================== |  27820/27821 |  99%
   {http://purl.org/dc/elements/1.1/}language: |=======================  |  26490/27821 |  95%
  {http://purl.org/dc/elements/1.1/}publisher: |===============          |  17647/27821 |  63%
   {http://purl.org/dc/elements/1.1/}relation: |===                      |   4342/27821 |  15%
     {http://purl.org/dc/elements/1.1/}rights: |                         |     23/27821 |   0%
     {http://purl.org/dc/elements/1.1/}source: |                         |      1/27821 |   0%
    {http://purl.org/dc/elements/1.1/}subject: |====================     |  22519/27821 |  80%
      {http://purl.org/dc/elements/1.1/}title: |=========================|  27821/27821 | 100%
       {http://purl.org/dc/elements/1.1/}type: |=======================  |  26101/27821 |  93%
```

Field to be test reconciled with OCLC Entity Pilot: **dc:creator**

Notes:
- 15,889 unique names in 27,821 records.
- 227 unique names without commas (mix of corporate names and not inverted personal names). Most personal names are in last name, first name form.
- 27 unique names with numbers, mostly dates (1 email address, few typos). These unique names with dates are given below (numbers beside each mean how many times they appear in the ECommons data) because Jason asked about them:
  - 2005 Winter Dairy Management Series
  - Bartlett, Samuel Colcord, 1817-1898
  - Blodgett, Henry, 1825-1903
  - Boone, William Jones, 1811-1864
  - Edkins, Joseph, 1823-1905
  - Favier, Alphonse, 1837-1905
  - Ghali, Waguih, d. 1969
  - Kushwaha1, H.L.
  - Laufer, Berthold, 1874-1934
  - Legge, James, 1815-1897
  - Medhurst, Walter Henry, 1796-1857
  - Montucci, Antonio, 1762-1829
  - Mullens, Joseph, 1820-1879
  - New York State 4-H Camping Program
  - Pakenham-Walsh, William Sandford, Rev, 1868-1960
  - Parvus, 1867-1924
  - Philip, Robert, 1791-1858
  - Salisbury, Edward Elbridge, 1814-1901
  - Schereschewsky, Samuel Isaac Joseph, Bp., 1831-1906
  - Smith, Arthur Henderson, 1845-1932
  - Speer, Robert Elliott, 1867-1947
  - Stevens, William Bacon, Bp., 1815-1887
  - Taylor, James Hudson, 1832-1905
  - Wilson, Alpheus Waters, Bishop, 1834-1916
  - Winter Dairy Management 2008
  - Wylie, Alexander, 1815-1887
  - mwc34@cornell.edu, John
- some corporate names following LC heading form
- 71 unique headings have parenthesis. Many include middle names or full names in parenthesis. Some include qualifiers or role terms in parenthesis (uncertain if authority record headings qualifiers or concatenated role terms, looks to be mix of both).

**All unique values in that field with counts are in [ECommonsCreatorsUnique.txt](ECommonsCreatorsUnique.txt)**

##Matching Process

**Proposal**: Personal names (primary focus here) are best automatically matched using:

1. life dates (in OCLC Entity response, id.loc.gov, VIAF, Wikidata, ...). With exact match here and above average score for matching name strings (this needs to be firmed down as number ranges to both OCLC Entities score and other string matching possibilities)
2. Well above average score for matching name strings and one or more of the following:
  a. >90% subject matching (subjects in OCLC Entity response, original DC records, Wikidata...)
  b. >90% affiliation matching (publishers in original DC records *for this example*, 373 in id.loc.gov MARC response, 510 in VIAF, wdt:P108 in wikidata... (ISNI seems to repeat other data sources' affiliations))
  c. Matching in some way of role terms/relator codes? Need to explore further.
  d. Other?
3. Match of URI in source data (not seeing any so far in the original DC records for this example) with any/multiple of OCLC Entity SameAs URIs or identifiers from those URIs (i.e. the n12344556 from id.loc.gov URI).

This matching could occur without Entity pilot, but that provides a good starting point for exploring a number of data sources. What could help with this jumping off point:

1. Putting sameAs links in entity search response. This could help simplify somewhat this process, as well as maybe help with secondary de-duping of OCLC Entity Search responses.
2. Providing multi-index searching (being able to search name and associated dates from the beginning to get better results, matching)
3. Allowing fuzzy matching parameters to capture name labels that also have other information attached in the same field (as often happens with non-MARC metadata). Examples: names with dates, role terms, etc. Otherwise, this requires (per usual, so its not more effort than regular metadata matching and enhancement work) normalization work before running against OCLC Entity search API for decent results.

With the Results CSV provided here, the plan is to review and see if these matching points could work. Any fields with 'CUL score' in them means the script does basic levenshtein text matching of a field in the DC record and a field returned from one of the authorities/external data sources.

##Entities.py

This is built to, I hope, become the basis for a metadata entity matching python library that can work with common external library data sources - hence the preliminary work with classes (to be broken out into modules). Any feedback welcome, though its a work in progress.

##Results.csv

Guide to fields in CSV reports generated:

Each row is based on the separate dc:creator field instances to be reconciled. It is not a unique instance of every dc:creator field across the dataset as other contextual information from the record is being used for name entity matching rankings (title of work, affiliation, subjects, publication date...).

  - "record_identifier": oai record identifier for ecommons DC record. Used as way to confirm entity matching updates pathway.
  - "ecommons_entity_name": name of field to be matched. For ecommons DC records, using dc:creator, and all instances are literals/text strings. Would like to test with set also containing URIs or other identifiers next.
  - "ecommons_title": title of work described in the ecommons DC record.
  - "ecommons_title_year": year of publication of the work.
  - "ecommons_subject":
  - "ecommons_publisher":
  - "search_url"
  - "OCLC_result[n]_preflabel"
  - "OCLC_result[n]_birthdate"
  - "OCLC_result[n]_deathdate"
  - "OCLC_result[n]_score"
  - "OCLC_result[n]_subject"
  - "OCLC_result[n]_subject_CUL_score"
  - "OCLC_result[n]_OCLC_URI"
  - "OCLC_result[n]_LoC_preflabel"
  - "OCLC_result[n]_LoC_URI"
  - "OCLC_result[n]_LoC_birthdate"
  - "OCLC_result[n]_LoC_deathdate"
  - "OCLC_result[n]_LoC_affiliation_CUL_score"
  - "OCLC_result[n]_VIAF_URI"
  - "OCLC_result[n]_VIAF_title_CUL_score"
  - "OCLC_result[n]_VIAF_affiliation_CUL_score"
  - "OCLC_result[n]_ISNI_URI"
  - "OCLC_result[n]_Wiki_URI"
