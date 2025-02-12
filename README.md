# Azure-Data-Factory

This repository contains two Azure Data Factory (ADF) projects designed to manage and transform data in Azure Blob Storage using pipelines and mapping data flows.

---

## Project 1: CSV Sales Data Files

### Objective

The goal of this pipeline is to copy all CSV sales data files from a source container to a sink container in Azure Blob Storage, while organizing them in a hierarchical folder structure (`year/month.csv`).

### Steps

#### 1. File Setup in Blob Storage

1. Place all CSV files in the `source-container`.
2. Create a `sink-container` for storing the output files.

#### 2. Azure Data Factory Configuration

##### 2.1 Linked Services

- Create a linked service to connect Azure Data Factory with the source and sink Blob Storage containers.

##### 2.2 Datasets

- **Source Dataset**: Configure with parameters to dynamically fetch files from the source container.
- **Sink Dataset**: Configure to store files in the hierarchical structure in the sink container.

##### 2.3 Pipeline Activities

- **Activity 1: Get Metadata**
  - Retrieve the metadata of the source container.
- **Activity 2: Filter**
  - Filter to retrieve all CSV files from the metadata.
- **Activity 3: For Each Loop**
  - Iterate over the filtered files and copy them using the `Copy Data` activity.
  - **Copy Data Configuration**:
    - **Source**: Use the source dataset with parameters.
    - **Sink**: Organize the files in the `sink-container` using the hierarchy `year/month.csv`.

##### Validation and Execution

- Debug the pipeline.
- Validate and run the pipeline to ensure all files are copied and organized correctly in the sink container.

---

## Project 2: Transform and Analyze Sales Dataset

### Objective

This pipeline transforms a sales dataset (`dataset.xlsx`) using Mapping Data Flow, applies business rules, and generates insights such as:

1. Filtering revenue greater than \$2000.
2. Identifying the age group with the highest revenue, profit, and profit margin.
3. Storing the transformed data in CSV format.

### Steps

#### 1. File Setup in Blob Storage

1. Place the input Excel file (`dataset.xlsx`) in the `source-container`.
2. Create a `sink-container` for storing the transformed output.

#### 2. Azure Data Factory Configuration

##### 2.1 Linked Services

- Create a linked service to connect Azure Data Factory with the Blob Storage containers.

##### 2.2 Datasets

- **Source Dataset**: Configure to fetch the `dataset.xlsx` file from the source container.
- **Sink Dataset**: Configure to store the transformed data in CSV format in the sink container.

##### 2.3 Pipeline Activities

1. **Validate Source File**
   - **Activity: Get Metadata**: Validate the presence of the source file.
   - **Activity: If Condition**:
     - **True**: Proceed with data processing.
     - **False**: Wait for 10 seconds, then fail the activity.

2. **Mapping Data Flow**
   - **Source Transformation**: Import data from the source dataset.
   - **Select Transformation**: Select necessary columns.
   - **Derived Column Transformation**: Create new calculated columns if required.
   - **Filter Transformation**: Retain rows where revenue is greater than \$2000.
   - **Aggregate Transformation**: Calculate metrics to identify the age group with the highest revenue, profit, and profit margin.
   - **Sort Transformation**: Sort data for better organization.
   - **Sink Transformation**: Store the transformed data as a CSV file in the sink container.

##### Validation and Execution

- Debug and validate the pipeline.
- Run the pipeline to generate the transformed and analyzed dataset.

