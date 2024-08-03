# Secondary Metabolites of Bacterai Data Processing and Analysis Workflow

This document provides a comprehensive overview of the workflows for processing and analyzing data related to PubMed articles, chemicals, proteins, and interactions.

## Table of Contents
1. [Handling PMCID Values](#task1-handling-pmcid-values)
2. [Mapping PMIDs to PMCIDs](#task2-mapping-pmids-to-pmcids)
3. [Incorporating Additional Data](#task3-incorporating-additional-data)
4. [Extracting Sentences from PubMed](#task4-extracting-sentences-from-pubmed)
5. [Finding Available Datasets](#task5-finding-available-datasets)
6. [Retrieving Protein Data from UniProt](#task6-retrieving-protein-data-from-uniprot)
7. [Dataset Documentation](#task7-dataset-documentation)
8. [Identifying Responsible Proteins](#task8-identifying-responsible-proteins)
9. [Finding Chemical Drug Data](#task9-finding-chemical-drug-data)
10. [Data Processing Scripts](#task10-data-processing-scripts)
11. [Pathways Extraction and Analysis](#task11-pathways-extraction-and-analysis)
12. [Extremophile Classification with BioBERT](#task12-extremophile-classification-with-biobert)
13. [Sentence Summarization](#task13-sentence-summarization)
14. [Data Aggregation from UniProt](#task14-data-aggregation-from-uniprot)
15. [Chemical-Chemical Interaction Explorer](#task15-chemical-chemical-interaction-explorer)
16. [Gene-Gene Interaction Graph](#task16-gene-gene-interaction-graph)
17. [Biological Knowledge Graph](#task17-biological-knowledge-graph)

---

## Task1: Handling PMCID Values

**File:** `final_result_GENES.csv`

**Description:**
- This task involves removing the 'PMC' prefix from the `PMCID` column in the dataset to standardize the identifier format.
- The cleaned data is saved as `Genes_RemovedPMD.csv`.

---

## Task2: Mapping PMIDs to PMCIDs

**File:** `Task3_Species_PressureDeepSea.csv`

**Description:**
- This step creates a mapping between `PMID` and `PMCID` by matching entries from `final_result_GENES.csv`.
- The result is saved in `check.csv`, which includes `PMID` and its corresponding `PMCID`.

---

## Task3: Incorporating Additional Data

**File:** `Task3_Species_PressureDeepSea.csv`

**Description:**
- This task extends the previous mapping by including additional columns from `Task3_Species_PressureDeepSea.csv`.
- The combined dataset is saved as `final_result_species.csv`, which incorporates extra information alongside the `PMID` and `PMCID` mapping.

---

## Task4: Extracting Sentences from PubMed

**File:** `Species_RemovedPMD.csv`

**Description:**
- This task extracts relevant sentences related to chemicals from PubMed articles using the `Give_Sentences_PMC` function.
- The sentences are collected and saved in `Species_Sentences.csv`, with each entry including details about the chemicals and the associated sentences.

---

## Task5: Finding Available Datasets

**Objective:**
- Locate and document available datasets from the internet.

---

## Task6: Retrieving Protein Data from UniProt

**Data to Retrieve:**
- **Entry**: UniProt accession number of the protein.
- **Entry Name**: The unique name assigned to the protein entry.
- **Protein Names**: List of names associated with the protein.
- **Gene Names**: List of gene names related to the protein.
- **Length**: Length of the protein sequence.
- **PubMed ID**: Identifiers for publications associated with the protein.
- **GeneID**: Identifier for the gene.

---

## Task7: Dataset Documentation

**Overview:**
- This dataset includes details about various publications related to our research.

**Columns:**
- **Name**: The title or name of the dataset.
- **Description**: A brief summary or description of the dataset.
- **Publication Year**: The year in which the publication was released.
- **Publication Link**: The URL where the publication can be accessed.

**Purpose:**
- Helps in identifying and accessing relevant publications for further research and analysis.

---

## Task8: Identifying Responsible Proteins

**Overview:**
- The goal is to identify proteins responsible for specific genes based on the dataset provided.

**Columns in the Dataset:**
- **Gene**: The gene of interest.
- **Protein**: The associated protein with the gene.
- **Description**: A description of the gene or protein.
- **Link**: A link to additional information or resources about the gene or protein.
- **Publication Link**: A link to the publication that provides further details or evidence about the gene-protein relationship.

**Steps:**
1. Review Dataset: Examine the dataset for entries that specify genes and their associated proteins.
2. Verify Information: Check the provided links and descriptions to confirm the responsible proteins.
3. Identify Proteins: Note the proteins listed for each gene.
4. Document Findings: Record the proteins responsible for each gene and link to relevant publications.

**Purpose:**
- Understand the role of specific proteins in relation to genes and support further research and validation of biological functions.

---

## Task9: Finding Chemical Drug Data

**Objective:**
- Locate and document data related to chemical drugs, including their names, IDs, references, and trial phases.

**Data Fields:**
- **Chemical Name**: The name of the chemical drug.
- **Chemical ID**: The unique identifier assigned to the chemical drug.
- **Reference**: The source or reference where the chemical drug information is obtained.
- **Phase of Trial**: The phase of clinical trial (e.g., Phase I, Phase II, Phase III) in which the drug is currently or was previously involved.

**Steps:**
1. Gather Data: Collect information from reliable sources or databases about chemical drugs.
2. Extract Information:
   - **Chemical Name**: Record the name of each drug.
   - **Chemical ID**: Find and list the unique IDs associated with each drug.
   - **Reference**: Document the sources or references used for obtaining the data.
   - **Phase of Trial**: Identify and note the clinical trial phases for each drug.
3. Organize Data: Structure the data into a table or format for easy access and analysis.

**Purpose:**
- Track and understand the development status of chemical drugs, facilitating research and clinical decision-making.

---

## Task10: Data Processing Scripts

This repository contains scripts for merging and processing various biological datasets. Each script merges different types of data and extracts relevant interaction types and regulations.

### 1. **Gene_to_Chemical.py**
   - **Purpose**: Merges gene and chemical data, extracts interaction types and regulations, and saves the result as `Gene_to_Chemical.csv`.
   - **Key Steps**:
     ```python
     # Load DataFrames
     df1 = pd.read_csv(file1_path)
     df2 = pd.read_csv(file2_path)

     # Merge DataFrames
     merged_df = pd.merge(df1, df2, on='PMID', how='inner')

     # Define interaction and regulation keywords
     interaction_keywords = ['Inhibition', 'Activation', 'Proliferation', 'Allosteric', 'Agonist', 'Antagonist']
     regulation_keywords = ['(?:Up(?:-regulated)?)', 'Down(?:-regulated)?']

     # Process and save data
     final_df.to_csv(output_path, index=False)
     ```

### 2. **Gene_to_Disease.py**
   - **Purpose**: Merges gene and disease data, extracts interaction types and regulations, and saves the result as `Gene_to_Disease.csv`.
   - **Key Steps**:
     ```python
     # Load DataFrames
     df1 = pd.read_csv(file1_path)
     df2 = pd.read_csv(file2_path)

     # Merge DataFrames
     merged_df = pd.merge(df1, df2, on='PMID', how='inner')

     # Define interaction and regulation keywords
     interaction_keywords = ['Inhibition', 'Activation', 'Proliferation', 'Allosteric', 'Agonist', 'Antagonist']
     regulation_keywords = ['(?:Up(?:-regulated)?)', 'Down(?:-regulated)?']

     # Process and save data
     final_df.to_csv(output_path, index=False)
     ```

### 3. **Gene_to_Gene.py**
   - **Purpose**: Merges gene data with itself, extracts interaction types and regulations, and saves the result as `Gene_to_Gene.csv`.
   - **Key Steps**:
     ```python
     # Load DataFrames
     df1 = pd.read_csv(file1_path)
     df2 = pd.read_csv(file2_path)

     # Merge DataFrames
     merged_df = pd.merge(df1, df2, on='PMID', how='inner')

     # Define interaction and regulation keywords
     interaction_keywords = ['Inhibition', 'Activation', 'Proliferation', 'Allosteric', 'Agonist', 'Antagonist']
     regulation_keywords = ['(?:Up(?:-regulated)?)', 'Down(?:-regulated)?']

     # Process and save data
     final_df.to_csv(output_path, index=False)
     ```

### 4. **Chemical_to_Chemical.py**
   - **Purpose**: Merges chemical data with itself, extracts interaction types and regulations, and saves the result as `Chemical_to_Chemical.csv`.
   - **Key Steps**:
     ```python
     # Load DataFrames
     df1 = pd.read_csv(file1_path)
     df2 = pd.read_csv(file2_path)

     # Merge DataFrames
     merged_df = pd.merge(df1, df2, on='PMID', how='inner')

     # Define interaction and regulation keywords
     interaction_keywords = ['Inhibition', 'Activation', 'Proliferation', 'Allosteric', 'Agonist', 'Antagonist']
     regulation_keywords = ['(?:Up(?:-regulated)?)', 'Down(?:-regulated)?']

     # Process and save data
     final_df.to_csv(output_path, index=False)
     ```

---

## Task11: Pathways Extraction and Analysis

**Objective:**
- Extract pathways from datasets and analyze their associations with genes, chemicals, and diseases.

**Steps:**
1. **Extract Pathways**: Use the datasets to identify and extract relevant pathways.
2. **Analyze Associations**: Examine how these pathways relate to genes, chemicals, and diseases.
3. **Document Findings**: Save and document the pathways and their associations for further analysis.

**Tools:**
- **Scripts**: Pathways extraction and analysis scripts (e.g., `Pathways_Analysis.py`).

---

## Task12: Extremophile Classification with BioBERT

**Objective:**
- Classify extremophiles based on provided data using BioBERT for natural language processing.

**Steps:**
1. **Prepare Data**: Collect and preprocess text data related to extremophiles.
2. **Run Classification**: Use BioBERT to classify the extremophiles based on the data.
3. **Evaluate Results**: Review and evaluate the classification results for accuracy.

**Tools:**
- **BioBERT Model**: Pre-trained BioBERT model for classification tasks.

---

## Task13: Sentence Summarization

**Objective:**
- Summarize sentences related to biological data using summarization techniques.

**Steps:**
1. **Extract Sentences**: Collect relevant sentences from datasets.
2. **Summarize Sentences**: Use summarization algorithms or tools to create concise summaries.
3. **Document Summaries**: Save the summarized sentences for review and analysis.

**Tools:**
- **Summarization Tools**: Natural language processing tools for sentence summarization.

---

## Task14: Data Aggregation from UniProt

**Objective:**
- Aggregate protein data from UniProt for further analysis.

**Data to Aggregate:**
- **Entry**: UniProt accession number.
- **Entry Name**: Unique name assigned to the protein entry.
- **Protein Names**: List of names.
- **Gene Names**: List of gene names.
- **Length**: Protein sequence length.
- **PubMed ID**: Related publications.
- **GeneID**: Gene identifier.

**Steps:**
1. **Retrieve Data**: Collect protein data from UniProt.
2. **Aggregate Information**: Combine and organize the data for analysis.
3. **Save Data**: Save the aggregated data in a structured format.

**Tools:**
- **UniProt API**: For retrieving protein data.

---

## Task15: Chemical-Chemical Interaction Explorer

**Objective:**
- Explore and analyze interactions between different chemicals.

**Steps:**
1. **Gather Data**: Collect data on chemical interactions from relevant sources.
2. **Analyze Interactions**: Examine the interactions between chemicals.
3. **Visualize Data**: Create visualizations to represent chemical interactions.

**Tools:**
- **Data Visualization Tools**: Tools for creating visual representations of interactions.

---

## Task16: Gene-Gene Interaction Graph

**Objective:**
- Create a graph representing interactions between different genes.

**Steps:**
1. **Collect Data**: Gather data on gene interactions.
2. **Create Graph**: Use graphing tools to visualize gene interactions.
3. **Analyze Graph**: Examine the interactions and relationships between genes.

**Tools:**
- **Graph Visualization Tools**: Tools for creating and analyzing gene interaction graphs.

---

## Task17: Biological Knowledge Graph

**Objective:**
- Develop a knowledge graph representing biological entities and their relationships.

**Steps:**
1. **Define Entities**: Identify biological entities (e.g., genes, proteins, chemicals).
2. **Map Relationships**: Document relationships between these entities.
3. **Create Knowledge Graph**: Use graphing tools to create and visualize the knowledge graph.

**Tools:**
- **Knowledge Graph Tools**: Tools for constructing and visualizing biological knowledge graphs.
