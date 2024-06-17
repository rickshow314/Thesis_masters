# Queries performed using SPARQL:

## Query 1:
```bash
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
```bash
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
```bash
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
```bash
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
```bash
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX bao: <http://www.bioassayontology.org/bao#>
PREFIX nuccore: <https://www.ncbi.nlm.nih.gov/nuccore/>

SELECT ?metodo (COUNT(?metodo) AS ?cantidadUsos)
WHERE {
  ?variante obo:BFO_0000050 nuccore:NC_000017.11 ;  # 'part of' el cromosoma 17 usando el identificador NC_000017.11
            bao:BAO_0000207 ?metodo .  # 'has detection method' para obtener el método de detección
}
GROUP BY ?metodo
ORDER BY DESC(?cantidadUsos)
LIMIT 1

```
