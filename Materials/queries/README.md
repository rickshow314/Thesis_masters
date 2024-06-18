# Queries performed using SPARQL:

## Query 1: 
This query retrieves different types of genetic variants present in various databases. It helps in understanding the diversity of variant types and their classifications.
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX biolink: <https://w3id.org/biolink/vocab/>

SELECT ?tipoVariante (SAMPLE(?variante) as ?ejemplos)
WHERE {
  ?variante rdf:type ?tipoVariante .
  FILTER(STRSTARTS(STR(?tipoVariante), STR(obo:)))  # Asegura que los tipos sean URIs de OBO
}
GROUP BY ?tipoVariante
ORDER BY ?tipoVariante

```

## Query 2:
This query determines which chromosome most frequently contains deletions, using data from 1310 deletions found predominantly on chromosome 17.
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX obo: <http://purl.obolibrary.org/obo/>

SELECT ?cromosoma (COUNT(?delecion) AS ?cantidadDeleciones)
WHERE {
  ?delecion rdf:type obo:SO_0000159 ;  # SO_0000159 es el identificador para "deletion"
            obo:BFO_0000050 ?cromosoma .  # "part of" es la propiedad que vincula la variante al cromosoma
}
GROUP BY ?cromosoma
ORDER BY DESC(?cantidadDeleciones)
LIMIT 1

```

## Query 3:
This query identifies the most probable variant type associated with the gene ACTA2, highlighting the variant type that appears most frequently.
```sparql
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX bgw_hgene: <http://rdf.biogateway.eu/gene/9606/>

SELECT ?tipoVariante (COUNT(?tipoVariante) AS ?frecuencia)
WHERE {
  ?variante obo:RO_0002131 bgw_hgene:ACTA2 ;  # Relación 'overlap with gene'
            rdf:type ?tipoVariante .  # Obtiene el tipo de cada variante
  FILTER(STRSTARTS(STR(?tipoVariante), STR(obo:)))  # Asegura que los tipos sean URIs de OBO
}
GROUP BY ?tipoVariante
ORDER BY DESC(?frecuencia)
LIMIT 1

```

## Query 4:
This query explores the relationship between variants and a specific disease (Aortic aneurysm, OMIM: 617349), focusing on determining their clinical significance.
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX bgw_disease: <http://rdf.biogateway.eu/disease/>

SELECT ?variante ?significanciaClinica
WHERE {
  ?variante obo:RO_0003302 bgw_disease:617349 ;  # 'causes or contributes to condition' relacionado con la enfermedad 617349
           obo:RO_0002331 ?significanciaClinica .  # 'involved in' para obtener la significancia clínica
}

```

## Query 5:
The purpose of this query is to know to which biolink category chromosome 17 belongs and to check the existence of the object properties associated with Biolink and its federated query to check its operation.
# Local query
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX nuccore: <https://www.ncbi.nlm.nih.gov/nuccore/>
PREFIX biolink: <https://w3id.org/biolink/vocab/>

SELECT ?categoriaBiolink
WHERE {
  nuccore:NC_000017.11 biolink:category ?categoriaBiolink .
}

```
# Federated query
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX nuccore: <https://www.ncbi.nlm.nih.gov/nuccore/>
PREFIX biolink: <https://w3id.org/biolink/vocab/>

SELECT ?categoriaBiolink
WHERE {
  SERVICE <http://ssb4.nt.ntnu.no:23122/sparql> {
    nuccore:NC_000017.11 biolink:category ?categoriaBiolink .
  }
}
```
