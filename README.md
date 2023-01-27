# SPARQL-star-Benchmark

This repository contains the scripts and the queries for the RDF-star evaluation paper.

### Engines:
- [Apache Jena](https://jena.apache.org/): A free and open source Java framework for building Semantic Web and Linked Data applications. The framework supports the processing and quering of RDF-star. Read More [here](https://jena.apache.org/documentation/rdf-star/) 
- [Oxigraph](https://github.com/oxigraph): An open-source SPARQL database and some utility libraries. The engine supports the processing and querying of RDF-star.
- [Stardog](https://www.stardog.com/): The engine supports the processing of the RDF-star and its query language, SPARQL-star. The graph model includes the "Edge Properties" to support the RDf-star. Read More [here](https://docs.stardog.com/query-stardog/edge-properties)
- [GraphDB](https://graphdb.ontotext.com/): The engine supports the processing of the RDF-star and its query language, SPARQL-star. Read More [here](https://graphdb.ontotext.com/documentation/9.2/free/devhub/rdf-sparql-star.html).

### Folders: 
- Queries: contains the final list of variations that we included in contains the final list of variations that we extended from the REF benchmark and included in the paper. 
- REF: contains the original queries from REF benchmark. The list can be found [here](https://github.com/dgraux/RDFStarObservatory/tree/master/testSuits/REF-Benchmark/BKR)
- scripts: contains the bash files used to execute the queries for the four graph engines in addition to essential configurations.
