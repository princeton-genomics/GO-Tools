# Princeton GO Tools

**UNDER CONSTRUCTION**

This is a small collection of Gene Ontology tools developed at the Lewis-Sigler Institute at Princeton University over the years.

## Contents

1. **[Introduction](#intro)**
2. **[Dependencies](#dependencies)**
3. **[Roadmap](#roadmap)**
4. **[Publications](#publications)**
5. **[Citation](#citation)**
6. **[Links](#links)**
7. **[License](#license)**
8. **[Disclaimer](#disclaimer)**

---

## Introduction

The Gene Ontology (GO) project seeks to describe how genes encode biological functions using formal ontologies with a controlled vocabulary of terms and gene product annotations from GO Consortium members and other contributors. Generally, data is presented as a file describing the ontology (ie. gene_ontology.obo) and other files containing the species-specific annotations provided some database/project (ie. gene_association.pombase). Please see the [Gene Ontology Consortium](http://geneontology.org) and other sources in the [link section](#links) for more information.

Most of these tools depend on the [GO::TermFinder](http://search.cpan.org/dist/GO-TermFinder/) perl module by Gavin Sherlock and Shuai Weng at Stanford University and the **GO::View** perl module written by Shuai Weng. GO::TermFinder is described in **GO::TermFinder--open source software for accessing Gene Ontology information and finding significantly enriched Gene Ontology terms associated with a list of genes., Boyle et al, Bioinformatics (2004)**, available at [PubMed](https://www.ncbi.nlm.nih.gov/pubmed/15297299).

These tools are made publicly available through the [GMOD Project](http://www.gmod.org/).

Everything in this repository is Copyright (c) 2014 and 2017 Lewis-Sigler Institute, Princeton University.

### GOTermFinder

GOTermFinder is a tool for finding significant GO terms shared among a list of identifiers (ie. genes) in the selected annotation, helping you discover what they may have in common. It generates a p-value for each term as a measure of significance.

This was one of the first of the GO applications developed here, and has undergone many changes, by multiple developers, for over a decade (for better and for worse). It remains one of our most popular GO tools.

### GOTermMapper

GOTermMapper is a tool for mapping the granular GO annotations for your identifiers (ie. genes) to a set of broader, high-level GO parent terms (often referred to as GO slim terms), allowing you to bin them into broad categories. It is much faster and lighter weight than GOTermFinder, as it does not generate p-values for significance.

This was developed alongside GOTermFinder.

### LAGO

LAGO functions in much the same way as GOTermFinder, generating p-values for significance for each of the terms. However it is written in C for much greater efficiency. Performance varies depending on the parameters, annotation, etc., however in tests it was running 50 times faster (or more) for common queries while using down to 1/20 (or less) of system memory.

LAGO was developed much more recently to address the efficiency of GOTermFinder, especially for larger annotations, and to do common queries more quickly.

## Dependencies

* [GO::TermFinder 0.86](http://search.cpan.org/dist/GO-TermFinder/)
* graphviz 2.30.1-19 (there are often significant changes between versions)
* [map2slim](http://search.cpan.org/~cmungall/go-perl/scripts/map2slim) part of [go-perl](http://search.cpan.org/~cmungall/go-perl) (for GOTermMapper)

## Roadmap

In each of these directories, there may be a README file with a section containing instructions on what to change to get things working at your site.

* ***bin*** The perl applications are located here.
* ***src*** Contains the source code for LAGO, written in C.
* ***lib*** Contains additional perl modules.
* ***etc*** Contains configuration files.
* ***doc*** Includes tool-specific and other documentation.

Note that ***lib*** contains some files from GO::TermFinder and GO::View which were modified. These must override the files distributed with GO::TermFinder.

## Relevant publications

**GO::TermFinder--open source software for accessing Gene Ontology information and finding significantly enriched Gene Ontology terms associated with a list of genes., Boyle et al, Bioinformatics (2004)** [PubMed](https://www.ncbi.nlm.nih.gov/pubmed/15297299)

**The Gene Ontology (GO) database and informatics resource., Harris et al, Nucleic Acids Research (2004)** [PubMed](https://www.ncbi.nlm.nih.gov/pubmed/14681407)

## Citation

There is no direct citation for the contents of this repository. For
publications, please cite the original manuscripts above, and map2slim
and/or go-perl if relevant (if GOTermMapper is being cited). Also
please include the URL for our tools (http://go.princeton.edu) and/or
the URL for the specific tool that is relevant to your publication.

## Links

* [GO tools at Princeton LSI](http://go.princeton.edu)
* [GO::TermFinder](http://search.cpan.org/dist/GO-TermFinder/)
* [go-perl](http://search.cpan.org/~cmungall/go-perl)
* [Gene Ontology Consortium](http://geneontology.org)
* [GMOD Project](http://www.gmod.org/)

## License

Everything in this repository is made publicly available via the MIT License:

Copyright 2004 and 2017, Lewis-Sigler Institute, Princeton University

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Disclaimer

This application and all associated files are provided in good
faith. However, environments and circumstances vary and the user is
responsible for ensuring that they are operating correctly for their
own purposes. Neither the developer nor Princeton University nor it's
affiliates or institutions will be held liable for any use of these
files or associated documentation or third-party modifications or
applications of them whatsoever.

LAGO is currently considered to be in beta and is being actively
worked on. There are portions of the code containing alternate
implementations, or implementation ideas, and notes about things that
may need attention. Some portions of the code may be marked unused and
commented out for completeness or reference and not been thoroughly
tested or kept up-to-date. This will all be cleaned up before leaving
beta.
