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
