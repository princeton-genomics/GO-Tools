# GOTermFinder

## Contents

1. **[Features](#features)**
2. **[Basic usage](#basicUsage)**
3. **[Required files](#requiredFiles)**
4. **[Output files](#output)**

---

## Features

GOTermFinder is a tool for finding significant GO terms shared among a list of identifiers (ie. genes) in a selected annotation, helping you discover what they may have in common. It generates a p-value for each term as a measure of significance. A false discovery rate can be computed as well.

It applies a p-value cutoff, so that only terms with higher significance are reported, and can optionally do Bonferroni correction. Also, optionally, the background size used in the significance calculations can be adjusted, or a background list of identifiers can be provided.

The script provides, at a minimum, a tab-delimited list of terms, p-values, identifiers, and other information. The script can also generate a graph (a directed acyclic graph, or DAG), showing the terms and their relations to each other and the provided list of identifiers, using GraphViz, and tables in HTML format.

It is possible to filter the annotation and ontology to some degree. Aside from filtering by aspect, which is required, the annotation can be filtered by evidence code (using either an inclusive or exclusive list of codes), and the ontology can be filtered such that regulation links are not followed.

To improve processing time, the script can store and retrieve internal data objects, using Storable, which cuts down on initial parsing and background initialization considerably. These objects depend on several factors, such as the annotation, ontology, and aspect, and cannot be used with evidence code filtering and some other advanced options.

## Basic usage

The minimal arguments are:

-t <output directory> (defaults to /tmp)
-a <ontology aspect> (C|F|P)
-g <gene annotation file>
-f <ontology file> (defaults to gene_ontology.obo)
<file containing list of identifiers>

Process aspect, minimal output:

/usr/bin/perl GOTermFinder.pl -a P -g /data/gene_association.sgd -f /data/gene_ontology.obo -t /tmp/out genes.txt

There are several other options which are often useful:

-h (generate HTML table)
-i (generate DAG files and HTML image-mapped file)
-p (p-value cutoff, default 0.01)
-b <background population identifier list file>
-n <num gene products> (size of background)
-F (calculate false discovery rate (FDR))
-e [-]<evidence code list>
-l (do not follow regulation links)
-C "none"|"bonferroni" (p-value correction method, default is "bonferroni")

P-value cutoff of 0.001, background size 6468, make image and HTML files:

/usr/bin/perl GOTermFinder.pl -ih -p 0.001 -n 6468 -a P -g /data/gene_association.sgd -f /data/gene_ontology.obo -t /tmp/out genes.txt

Function aspect, background identifier list:

/usr/bin/perl GOTermFinder.pl -ih -a F -g /data/gene_association.sgd -f /data/gene_ontology.obo -t /tmp/out -b background.txt genes.txt

Compute FDR, exclude IEA and ND annotations:

/usr/bin/perl GOTermFinder.pl -ih -F -e -IEA,ND -a P -g /data/gene_association.sgd -f /data/gene_ontology.obo -t /tmp/out genes.txt

To support pre-parsed files:

-cache <path>
-write-cache

Save the pre-parsed objects in a cache file (basic options only):

/usr/bin/perl GOTermFinder.pl -write-cache -cache /tmp/sgd_P.bin -a P -g /data/gene_association.sgd -f /data/gene_ontology.obo

Use the cache in a query:

/usr/bin/perl GOTermFinder.pl -cache /tmp/sgd_P.bin -a P -g /data/gene_association.sgd -f /data/gene_ontology.obo -t /tmp/out genes.txt

(The -g and -f options are still required, possibly a bug, or possibly to validate the cache.)

There are many other options available, but they are mostly for edge-case usage.

## Input files

An annotation file in GAF format (and provided with the -g option), an ontology file (optionally specified with the -f option but defaults togene_ontology.obo), and an identifier list, with one identifier per line, are all required. These can be specified by absolute path. If the code has default directories configured correctly, and only the file names for the annotation and/or ontology are given, it will search those directories for them.

Additionally, the background population list may be provided with -b. It also expects one identifier per line. This defines the identifiers against which significance is measured, and should usually contain all identifiers in the query.

## Output files

Minimally, the program will produce a tab-delimited list of GO IDs, terms, p-values, annotated genes, and other information. Additionally, a term list file is generated. With -h, an HTML-formatted table is produced, with external links.

With -i, a DAG is created, in ps, png, and svg format. Also, an HTML file is created which contains the DAG with image-mapped links. (Much of this was implemented to support the web-based tool at http://go.princeton.edu.)

## Porting

Although the code has always been publicly available, and could be set up to run anywhere, it does require a small amount of local customization to get running. It isn't the most user-friendly thing either, as it was originally intended to be run only behind our web interface.

The most important change is the path to the lib directory of this distribution (in a "use lib" line near the top). Also, $goDir and $goParseDir can be modified. These define the default directories to look for the text annotation and ontology files and the pre-parsed object files, respectively. Also, $confFile may be defined with a path to a GO::View configuration file, if the defaults are inappropriate. All these settings are near the top of the script.

If needed, the $binDir and $libDir settings can be used to locate the binaries and libraries of the GraphViz package.
