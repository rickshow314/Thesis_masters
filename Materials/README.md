# Master's Thesis Resources

This directory contains all the resources needed for the master's thesis. The resources are organized in several subfolders, each of which contains specific files related to different aspects of the project.

## Structure of Directories

- `data/`: It contains the files belonging to the data to be exploited from the databases.
- `diagrams/`: It includes conceptual diagrams of the model and real cases.
- `scripts/`: Stores the scripts that standardize the data.
- `mapping/`: Contains the mapping files in YARRRML.
- `queries/`: Includes queries performed with SPARQL.

## Folder Description

### `data/`
This folder contains the data sets to be used in this work. Here are the data obtained from various databases such as dbVar, ClinVar and GWAS. Each file represents a representative sample of the data to speed up processing and keep the generated file size below 1 GB.

### `diagrams/`
In this folder you will find the conceptual diagrams of the RDF model and the real cases that will be used in this project. These diagrams are essential to understand the structure and relationship between the data.

### `scripts/`
This folder stores the scripts that have been developed to standardize the data. These scripts ensure that the data is consistent and can be integrated effectively.

### `mapping/`
It contains the mapping files generated using YARRRML (Yet Another RDF Rules Mapping Language). These files are crucial to transform the original data into RDF format.

### `queries/`
Here are the queries performed with SPARQL (SPARQL Protocol and RDF Query Language). These queries allow us to relate genetic variants with diseases, facilitating a better understanding and treatment of them.

## Resource Use

1. **Data**: Access the data sets in the `data/` folder and be sure to follow the specific instructions for each file.
2. **Diagrams**: Review the conceptual diagrams in `diagrams/` to understand the structure of the RDF model and the relationship between the different components.
3. **Scripts**: Execute the scripts in `scripts/` to standardize and prepare the data for RDF mapping.
4. **Mapping**: Uses the mapping files in `mapping/` to transform the standardized data into RDF triples.
5. **Queries**: Perform SPARQL queries using the files in `queries/` to obtain valuable information and perform comparative analysis.
