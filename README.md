
# On Benchmarking RDF-star triplestores with StarBench
**Title:** StarBench: Benchmarking RDF-star Triplestores

**Abstract:** RDF-star has rapidly gained popularity as a way to annotate RDF statements while avoiding the disadvantages of reification. Hence, a number of triplestores supporting this new standard have become available. Yet, it is difficult to assess the performance of each of the systems and to which degree they support RDF-star and the corresponding SPARQL-star query language. Hence, in this paper, we propose StarBench, a benchmark for testing SPARQL-star support and runtime performance. We ran StarBench on a number of state-of-the-art triplestores with RDF-star and SPARQL-star support and share our findings. Based on these findings, we highlight existing challenges and research opportunities.

**Submitted to** ISWC 2023 Resource track

### See our [website](https://relweb.cs.aau.dk/starbench) for more info.

# Overview
RDF-star is an extension of RDF that allows for more expressive relationships, enabling more powerful applications and use cases. Adoption of RDF-star may result in increased utilization of RDF triplestores capable of supporting its applications. Support for RDF-star in existing RDF triplestores allows for seamless integration, but further research is needed to enhance their capabilities. We developed StarBench, a SPARQL-star benchmark to evaluate RDF triplestores' performance in handling RDF-star and SPARQL-star queries. The evaluation revealed that certain RDF triplestores would benefit from optimization techniques specifically designed for RDF-star, emphasizing the need for additional research and development in this area.

## RDF Triplestores
We executed the following triplestores over our benchmark:
- [Apache Jena](https://jena.apache.org/): Version 4.7.0 with TDB version 2: We used the default configuration for the TDB loader. We used Fuseki for the server and curl to execute the queries.
- [Oxigraph](https://github.com/oxigraph): Version 0.3.16 using the project's docker image and curl to execute the queries.
- [Stardog](https://www.stardog.com/): Version 8.1.0, Default configurations except for the query timeout, we changed it from 3 seconds to 30 minutes (the timeout threshold for all the queries in our experiments).
- [GraphDB](https://graphdb.ontotext.com/): Version 10.0.2, installed as a standalone server and curl to execute the encoded queries.
- [AnzoGraph](https://cambridgesemantics.com/anzograph/): Version 2.5.16, installed as a standalone Jetty server and curl to execute the queries.
- [BlazeGraph](https://blazegraph.com/): Version 2.1.6, installed as a standalone Jetty server and curl to execute the queries.

AnzoGraph and BlazeGraph were not able to load the datasets, and have therefore been omitted from our experiments.
AnzoGraph threw a "too many properties" error, and BlazeGraph a Parsing error.

## Dataset & Queries
#### Dataset
The Biomedical Knowledge Repository (BKR) dataset (version 0.2), which is provided by the U.S. National Library of Medicine, has been represented in RDF-star format as part of the REF benchmark work carried out by Orlandi, Fabrizio, Graux, Damien, and O'Sullivan, Declan in 2020. The RDF-star representation of the BKR dataset is accessible at [zenodo](https://doi.org/10.5281/zenodo.3894745). The biomedical dataset comprises a total of 61,032,567 triples, including approximately 35 million distinct subjects, 8 million distinct objects, and over 33 million distinct predicates.
#### Queries
The queries can be seen in the [queries](https://github.com/dkw-aau/SPARQL-star-Benchmark/tree/main/Queries) directory and comprises 56 queries in 3 different categories, extended from the [REF benchmark](https://zenodo.org/record/4148888#.ZFjpOpFBwUE) queries P1-P23, S1-S22, and C1-C11. For more information on the queries, check out the full list of queries including detailed descriptions of the modifications on our [website](https://relweb.cs.aau.dk/starbench/#queries). 

## Getting Started with StarBench Benchmark
The following guide is based on setting up and running the benchmark over [Apache Jena](https://jena.apache.org/). Other systems will have slightly different commands to load the data and run the queries. Our GitHub repository contains [scripts](https://github.com/dkw-aau/SPARQL-star-Benchmark/tree/main/scripts) to run the benchmark over the four systems included in the paper (Jena, Oxigraph, Stardog, and GraphDB).

###  Step 1: Download and start the Fuseki server
Download the latest version of [Apache Jena and Fuseki](https://jena.apache.org/download/index.cgi) and unpack the binaries to your server.  
Use the TDB Loader to load the dataset to a TDB database as follows:
```
${jena-home}/bin/tdb2.tdbloader --loc ${db-dir} ${data}.ttls
```
Where `${jena-home}` is the directory of the Jena installation, `${db-dir}` is the directory of the database files, and `${data}.ttls` is the dataset TTLS file.
Afterwards, start the Fuseki server using the following command:
```
java -jar ${fuseki-home}/fuseki-server.jar --loc=${db-dir} /rdfstar
```
Where `${fuseki-home}` is the directory of the Fuseki installation.

**To ease loading the data and running the server, you can use the provided server-side [script](https://github.com/dkw-aau/SPARQL-star-Benchmark/tree/main/scripts/server/Jena) for Jena as follows:**
```
bash scripts/server/Jena ${jena-home} ${fuseki-home} ${db-dir} ${data}
```
Similar scripts have been provided for the other engines included in our experiments.

### Step 2: Run the StarBench queries from the client machine

On the client machine: Download the [queries](https://github.com/dkw-aau/SPARQL-star-Benchmark/tree/main/Queries). To execute a query over the Fuseki endpoint, run the following command:

```
curl --silent -X POST -H "Accept: application/sparql-results+json" -H "Content-Type: application/sparql-query" \
            --data "${query}" http://${ip}:3030/rdfstar/query
```
Where `${query}` is the SPARQL-star query to execute and `${ip}` is the IP address of the server.

**To ease running the queries over the server loaded above, you can use the provided client-side [script](https://github.com/dkw-aau/SPARQL-star-Benchmark/tree/main/scripts/client/Jena) for Jena as follows:**
```
bash scripts/client/Jena ${queries} ${ip}
```
Where `${queries}` is the directory containing the queries.  
Similar scripts have been provided for the other engines included in our experiments.

##### Every triplestore has its own unique method and command for loading datasets, preparing them for querying, and executing the queries. To ensure the correct procedure, refer to the associated script for each triplestore engine, which can be found in the [scripts](scripts) folder. 


### Folders: 

- [Queries](Queries): contains the final list of queries that we extended from the REF benchmark and included in the paper. 
- [REF](REF): contains the original queries from REF benchmark. The list can be found [here](https://github.com/dgraux/RDFStarObservatory/tree/master/testSuits/REF-Benchmark/BKR)
- [scripts](scripts): contains the bash files used to execute the queries for the four graph engines in addition to essential configurations.
	- [server](scripts/server) contains the scripts for running the server-side and loading in the datasets
	- [client](scripts/client) contains the client-side scripts to execute the queries over the server-side.

#### Licenses
Queries distributed under CC-BY 4.0 license, scripts/code under ASL-2.0 license. The directories each contain their respective licenses.

