# SPARQL Unicorn Wikidata Plugin

**This plugin adds a GeoJSON layer from a Wikidata SPARQL query.**

* qgisMinimumVersion=3.0
* version=0.2
* author=SPARQL Unicorn
* email=rse@fthiery.de

use the following commands in the `Administrator:OSGeo4W Shell` to install required libs for python 2.7 and python 3.x

* https://youtu.be/94W51WuDKzA
 * install in py2: python -m pip install `package`
 * switch from py2 to py3: py3_env
 * install in py3: python -m pip install `package`
* `geomet`, `geojson`, `SPARQLWrapper`

## Sample query

*What is needed?*

* ?label
* ?geo (lat/lon)
* ?item

### Ogham Stones

```sql
SELECT ?label ?geo ?item WHERE {
  ?item wdt:P31 wd:Q2016147;
    wdt:P361 wd:Q67978809;
    wdt:P195 ?collection.
  OPTIONAL { ?item wdt:P625 ?geo. }
  OPTIONAL {
    ?item rdfs:label ?label.
    FILTER((LANG(?label)) = "en")
  }
  OPTIONAL {
    ?collection rdfs:label ?collectionLabel.
    FILTER((LANG(?collectionLabel)) = "en")
  }
}
ORDER BY (?label)
```

### Hospitals

```sql
SELECT * WHERE {
  ?item ((wdt:P31*)/(wdt:P279*)) wd:Q16917;
    wdt:P625 ?geo;
    rdfs:label ?label.
  FILTER((LANG(?label)) = "en")
}
```
