<img src="assets/arpedia-logo.png" alt="Arpedia Logo" width="whatever" height="199px" align="left" >

# Arpedia Microservice

The ETL data pipeline, indexing and REST API for the Arpedia microservice

Moving all the data pipeline out of the Kadist repository and into this one which has no UI requirements. All the API calls are for the Arpedia client and are RESTfull, but no view templates here.

The ETL pipeline consists of three parts. Data capture, including scrapes or data dumps, the transformations that occur to unify schemas, enrich data, assign fingerprints, and finally the indexing itself.

The fingerprints are created from an annotated corpus (Kadist) which using techniques like feature reduction and LDA/LSI produces a semantic fingerprinted corpus. Untagged documents (which come from art work descriptions) are then matched to this corpus using standard search techniques (through Lucene) and the fingerprints from those matches are used to join with other untagged content. 

## Data

Each object in the index has a type, each with a format:

# artwork, optional physical (has a location property)
```
{
	"permalink": "mandatory::<absolute url>",
	"images": [{
		"caption": "mandatory::<text>",
		"url": "mandatory::<absolute url>"
	}],
	"title": "mandatory::<title>",
	"artist": "mandatory::<artist name>",
	"artist_data": "optional::<unstructured text>",
	"location": "optional::<structured location code>",
	"description": "mandatory::<unstructured text>",
	"medium": "optional::<unstructured text>",
	"acquisition": "optional::<unstructured text>",
	"dimensions": "optional::<unstructured text>",
	"tags": [
		"optional::<unstructured text>"
	],	"creation_year": "optional::<year number",
	"collection": "mandatory::<structured text>"
}
```

# video, publication
```
{
	"permalink": "mandatory::<absolute url>",
	"images": [{
		"caption": "mandatory::<text>",
		"url": "mandatory::<absolute url>"
	}],
	"title": "mandatory::<title>",
	"creator": "mandatory::<creator name>",
	"creator_data": "optional::<unstructured text>",
	"description": "mandatory::<unstructured text>",
	"tags": [
		"optional::<unstructured text>"
	],	"creation_year": "optional::<year number",
	"collection": "mandatory::<structured text>"
}
```

# temporal object (event, exhibition), optional physical (has a location property)
```
{
	"permalink": "mandatory::<absolute url>",
	"images": [{
		"caption": "mandatory::<text>",
		"url": "mandatory::<absolute url>"
	}],
	"title": "mandatory::<title>",
	"start_date": "mandatory::MM/DD/YY>",
	"end_date": "mandatory::<MM/DD/YY>",
	"location": "optional::<structured location code>",
	"description": "mandatory::<unstructured text>",
	"tags": [
		"optional::<unstructured text>"
	],
	"collection": "mandatory::<structured text>"
}
```
