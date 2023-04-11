# On Benchmarking RDF-star triplestores with StarBench

# Overview
RDF-star is an extension of RDF that allows for more expressive relationships, enabling more powerful applications and use cases. Adoption of RDF-star may result in increased utilization of RDF triplestores capable of supporting its applications. Support for RDF-star in existing RDF triplestores allows for seamless integration, but further research is needed to enhance their capabilities. We developed StarBench, a SPARQL-star benchmark to evaluate RDF triplestores' performance in handling RDF-star and SPARQL-star queries. The evaluation revealed that certain RDF triplestores would benefit from optimization techniques specifically designed for RDF-star, emphasizing the need for additional research and development in this area.

## RDF Triplestores
- [Apache Jena](https://jena.apache.org/): A free and open source Java framework for building Semantic Web and Linked Data applications. The framework supports the processing and quering of RDF-star. Read More [here](https://jena.apache.org/documentation/rdf-star/) 
- [Oxigraph](https://github.com/oxigraph): An open-source SPARQL database and some utility libraries. The engine supports the processing and querying of RDF-star.
- [Stardog](https://www.stardog.com/): The engine supports the processing of the RDF-star and its query language, SPARQL-star. The graph model includes the "Edge Properties" to support the RDf-star. Read More [here](https://docs.stardog.com/query-stardog/edge-properties)
- [GraphDB](https://graphdb.ontotext.com/): The engine supports the processing of the RDF-star and its query language, SPARQL-star. Read More [here](https://graphdb.ontotext.com/documentation/9.2/free/devhub/rdf-sparql-star.html).

## Dataset

 Biomedical Knowledge Repository (BKR) dataset provided by the U.S. National Library of Medicine. The RDF-star representation of the BKR dataset created in the REF benchmark work~\cite{orlandi2021benchmarking} The biomedical dataset comprises a total of 61,032,567 triples, including approximately 35 million distinct subjects, 8 million distinct objects, and over 33 million distinct predicates.

## Getting Started with StarBench Benchmark
This repository contains the scripts and the queries for the StarBench evaluation. To replicate the evaluation follow the commands of running each engine in each associated script:

### Step 1: Loading RDF-star dataset into the RDF triplestore:

Each triplestores has a different 

### Step 2: Run StarBench queries:

### Folders: 
- [Queries](Queries): contains the final list of variations that we included in contains the final list of variations that we extended from the REF benchmark and included in the paper. 
- REF: contains the original queries from REF benchmark. The list can be found [here](https://github.com/dgraux/RDFStarObservatory/tree/master/testSuits/REF-Benchmark/BKR)
- [scripts](scripts): contains the bash files used to execute the queries for the four graph engines in addition to essential configurations.
