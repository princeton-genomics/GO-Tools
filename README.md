# Princeton GO Tools

**UNDER CONSTRUCTION**

This is a small collection of Gene Ontology tools developed at the Lewis-Sigler Institute at Princeton University over the years.

## Contents

1. **[Introduction](#intro)**
2. **[Roadmap](#roadmap)**
3. **[History](#history)**
4. **[Publications](#publications)**
5. **[Links](#links)**
6. **[License](#license)**

---

## Introduction

The [GO Help Page at SGD](http://www.yeastgenome.org/help/function-help/gene-ontology-go) gives the following description of the Gene Ontology:

"The Gene Ontology (GO) project was established to provide a common language to describe aspects of a gene product's biology. The use of a consistent vocabulary allows genes from different species to be compared based on their GO annotations. The objective of GO is to provide controlled vocabularies for the description of the biological process, molecular function, and cellular component of gene products. These terms are to be used as attributes of gene products by organism databases, facilitating uniform queries across them. The controlled vocabularies of terms are structured to allow annotation of gene products to GO terms at varying levels of detail and to query for gene products that are involved in similar processes, function and components." 

Most of these tools depend on the [GO::TermFinder](http://search.cpan.org/dist/GO-TermFinder/) perl module by Gavin Sherlock and Shuai Weng at Stanford University and the **GO::View** perl module written by Shuai Weng. GO::TermFinder is described in **GO::TermFinder--open source software for accessing Gene Ontology information and finding significantly enriched Gene Ontology terms associated with a list of genes.**, ***Boyle et al, Bioinformatics (2004)***, available at [PubMed](http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=15297299).

These tools are made publicly available through the [GMOD Project](http://www.gmod.org/).

Everything in this repository is Copyright (c) Lewis-Sigler Institute, Princeton University.

### GOTermFinder

GOTermFinder is a tool for finding significant GO terms shared among a list of identifiers (ie. genes) in the selected annotation, helping you discover what they may have in common. It generates a p-value for each term as a measure of significance.

This was one of the first of the GO applications developed here, and has undergone many changes, by multiple developers, for over a decade (for better and for worse). It remains one of our most popular GO tools.

### GOTermMapper

GOTermMapper is a tool for mapping the granular GO annotations for your identifiers (ie. genes) to a set of broader, high-level GO parent terms (often referred to as GO slim terms), allowing you to bin them into broad categories. It is much faster and lighter weight than GOTermFinder, as it does not generate p-values for significance.

This was developed alongside GOTermFinder.

### LAGO

LAGO functions in much the same was as GOTermFinder, generating p-values for significance for each of the terms. However it is written in C for much greater efficiency. Performance varies depending on the parameters, annotation, etc., however in tests it was running 50 times faster (or more) for common queries while using down to 1/20 (or less) of system memory.

LAGO was developed much more recently to address the efficiency of GOTermFinder, especially for larger annotations, and to do common queries more quickly.

## Roadmap

* ***bin*** The perl applications are located here.
* ***src*** Contains the source code for LAGO, written in C.
* ***lib*** Contains additional perl modules.
* ***etc*** Contains configuration files.
* ***doc*** Includes tool-specific and other documentation.

Note that ***lib*** contains some files from GO::TermFinder and GO::View which were modified. These must override the file distributed with GO::TermFinder.

## History

## Publications

## Links

## License
