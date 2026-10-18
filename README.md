# Peplife2_Webserver

<img width="959" height="542" alt="Peplife2 home" src="https://github.com/user-attachments/assets/9cafba9f-ed93-466c-b831-f58f004222dc" />

# PEPlife2: An Updated Repository of the Half-Life of Peptides and Proteins

[![DOI](https://img.shields.io/badge/DOI-10.3390%2Fimmuno6020026-blue)](https://doi.org/10.3390/immuno6020026)
[![Journal](https://img.shields.io/badge/Journal-Immuno%20(MDPI)-green)](https://www.mdpi.com/2673-5601/6/2/26)
[![Web Server](https://img.shields.io/badge/Web%20Server-Live-orange)](https://webs.iiitd.edu.in/raghava/peplife2/)
[![License: CC BY](https://img.shields.io/badge/Data%20License-CC%20BY-lightgrey)](https://creativecommons.org/licenses/by/4.0/)

**PEPlife2** is a manually curated database of experimentally determined half-lives of peptides and proteins, together with their sequences, chemical modifications, structures, assays and experimental conditions. It is an updated version of the original PEPlife database (2016) and is freely available through a responsive web interface and a REST API.

- **Web server:** https://webs.iiitd.edu.in/raghava/peplife2/
- **REST API:** https://webs.iiitd.edu.in/raghava/peplife2/api/rest.html
- **Paper:** https://www.mdpi.com/2673-5601/6/2/26
- **Preprint:** https://doi.org/10.1101/2025.05.13.653654

## Why this matters

Most therapeutic peptides are short-lived in vivo (typically a few minutes) because of proteolytic degradation and rapid renal clearance, which limits bioavailability and clinical efficacy. Strategies such as cyclization, D-amino acid substitution, terminal modification, lipidation and PEGylation can extend half-life, but the evidence is scattered across papers and patents. PEPlife2 brings this evidence into one searchable resource to support peptide therapeutics, pharmacokinetics, vaccine design and immunotherapy research.

## Database at a glance

| Item | Count |
|---|---|
| Total entries | **4,500** |
| Newly curated entries | 2,300 (2,046 from 449 research articles, 254 from 81 granted patents) |
| Entries carried over from PEPlife | 2,200 |
| Unique peptide sequences | 1,673 |
| Unique protein sequences | 257 |
| Predicted/retrieved structures | 432 unmodified, 349 modified |

Sequences of 50 residues or fewer are treated as peptides, and longer sequences as proteins (up to 3,611 residues).

## Features

- **Search:** by peptide name, sequence, modification type or physical formulation strategy.
- **Browse:** by peptide length, organism, media, modification type, assay type and publication year.
- **Analysis tools:**
  - BLAST and Smith-Waterman similarity search
  - Peptide Mapping
  - Sequence Alignment (CLUSTALW)
  - Structural Alignment (MUSTANG, upload a PDB file)
- **Download:** the full dataset in CSV format.
- **REST API:** programmatic access to the data.
- **MAP format support:** residue-level tags for chemical modifications, non-standard amino acids, binding sites and mutations.
- **Structures:** experimental structures from the PDB where available, otherwise predicted with PEPstrMOD (5 to 40 residues) or I-TASSER (more than 40 residues), with secondary structure assigned by DSSP.

## Data fields

Each entry records: PubMed ID, sequence, peptide name, sequence length, N-terminal modification, C-terminal modification, structural type (linear/cyclic), chirality, chemical modification, peptide origin, biological activity, experimentally determined half-life, assay type, sample or biological system, patent ID, route of administration, physical modification and SMILES. When the same peptide has several half-life values under different conditions, each value is stored as a separate entry.

## Data curation

1. PubMed was searched with the query `(half-life [Title/Abstract]) AND (peptide [Title/Abstract]) NOT Review` (May 2016 to November 2024), and granted patents were mined from The Lens.
2. The initial search retrieved 1,243 articles; about 950 were screened and 449 were curated. Of 291 patents, 81 were curated.
3. All information was extracted manually, and only peptides and proteins with experimentally reported half-life information were included.

## Architecture and tech stack

![PEPlife2 architecture](images/architecture.png)

| Layer | Technology |
|---|---|
| HTTP server | Apache 2.4.63 |
| Database | MySQL 5.7.31 |
| Backend | PHP 5.6.40 |
| Frontend | HTML5, CSS (Bootstrap 5.3.5), JavaScript |
| Analysis | BLAST 2.7.1, Smith-Waterman, CLUSTALW, MUSTANG |
| Structure | PDB, PEPstrMOD (AMBER 11, GROMACS 4.6.5), I-TASSER, DSSP |

The interface is responsive and works on desktops, tablets and smartphones.

## Using the data

**Web interface:** open the [web server](https://webs.iiitd.edu.in/raghava/peplife2/) and use the Search, Browse, Analysis or Download pages.

**API:** see the [REST API page](https://webs.iiitd.edu.in/raghava/peplife2/api/rest.html) for the available query fields and example requests.

## Comparison with PEPlife (2016)

| | PEPlife | PEPlife2 |
|---|---|---|
| Entries | 2,200 | 4,500 |
| Unique peptides | 1,193 | 1,673 |
| Unique proteins | 37 | 257 |
| Physical modifications (e.g. hydrogels) | No | Yes |
| Half-life type (distribution, activity) | No | Yes |
| Built-in alignment viewer | Needed Jalview | Results shown on the page |
| MAP format | No | Yes |

## Limitations

- Some modified peptides have no reported half-life for the native peptide, so direct comparison is not always possible.
- A few entries report only qualitative improvements ("stability increased") without numeric values; they are kept for their modification and formulation information.
- Structures for peptides with complex modifications (for example hydrocinnamate or chondroitin sulfate) are missing because force-field parameters are unavailable.
- Manual curation may still contain human error. Please check the original reference for important decisions.
