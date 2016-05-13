<img src="assets/arpedia-logo.png" alt="Arpedia Logo" width="whatever" height="200px" align="left" >

# Arpedia Microservice

The ETL data pipeline, indexing and REST API for the Arpedia microservice

Moving all the data pipeline out of the Kadist repository and into this one which has no UI requirements. All the API calls are for the Arpedia client and are RESTfull, but no view templates here.

The ETL pipeline consists of three parts. Data capture, including scrapes or data dumps, the transformations that occur to unify schemas, enrich data, assign fingerprints, and finally the indexing itself.

The fingerprints are created from an annotated corpus (Kadist) which using techniques like feature reduction and LDA/LSI produces a semantic fingerprinted corpus. Untagged documents (which come from art work descriptions) are then matched to this corpus using standard search techniques (through Lucene) and the fingerprints from those matches are used to join with other untagged content. 
