## Architecture Diagram Description
### Data Sources (Web Source)
- Data Source: NYC Yellow Taxi Dataset from a specified URL (https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)
- The CSV file contains tax zone maps and lookup tables.
- Yellow Taxi trip records (parquet files partitioned by year and month)

### Data extraction and storage
- Azure Storage Account. After extracting raw data from the web source, I stored it in an Azure Blob Container.

### Data Processing
#### Azure Databricks
- Databricks Compute Cluster: A scalable cluster for processing data. This is the processing engine for data cleaning and transformation.
- Data Cleaning and Transformation: Processed within Databricks, then stored back in the Azure Blob Container.

### Data Orchestration
- Multiple Azure Databricks Instances: These instances are scheduled to automatically perform data acquisition, cleaning, transformation, and storage tasks.

### Data Storage
- Azure Blob Storage: Stores both raw and cleaned data.

### Data Analytics
- Azure Data Analytics aggregates the cleaned data for further analysis.

### Dashboarding
- Looker, or PowerBI, visualizes the data from Azure Data Analytics to create interactive dashboards. I chose PowerBI because I am using Azure Cloud Services for the project's deployment. You can use any tool of your choice, considering its ease of use and feasibility.

### Data Flow
- The data starts from the Web Source, where it consists of multiple source files (CSV and Parquet). This data is ingested to Azure Blob Storage.
- Azure Blob Storage consists of the raw, unstructured dataset.
- Azure Databricks processes and cleans this data through different notebook instances and stores the cleaned data back in Azure Blob Storage.
- The data can be further fed into the Azure Database of your choice, for instance, MySQL, Cosmos DB, or Azure SQL DB to convert it into a structured format (I have depicted that in the deployment architecture).
- Azure Analytics then aggregates this cleaned data for further analysis.
- Finally, tools like Looker or PowerBI pull data from Azure Analytics for visualization and dashboarding.

### Rationale for the Scalable and Efficient Data Architecture in the NYC Taxi Dataset Project
The chosen architecture for the NYC Taxi dataset project leverages a combination of scalable cloud-based services and powerful analytics, ensuring efficient handling of large data volumes and insightful analysis. 
Starting with Azure Blob Storage for flexible and cost-effective raw data storage, the architecture employs Azure Databricks for its robust compute capabilities to clean and transform data. 
The use of multiple Databricks instances facilitates modular and automated data orchestration, allowing seamless data acquisition, processing, cleaning and storage back into Azure.  
I have followed the OOP techniques to keep the code clean and code reusable. Azure Analytics then integrates the cleaned and transformed data, providing scalable querying and data processing for advanced analytics. 
Finally, by connecting Looker or PowerBI to Azure Data Analytics, the architecture supports dynamic and interactive data visualization, making it easier to derive actionable insights. 
This setup not only optimizes the processing pipeline but also ensures that the system can scale and adapt to growing data volumes and complexity, aligning perfectly with the project's needs for comprehensive data analysis and visualization.

### The trade-offs involved in designing the NYC Taxi Dataset architecture are significant.
Designing the architecture for the NYC Taxi dataset project involved several trade-offs to balance performance, cost, scalability, and complexity:

Cost vs. performance:
- Azure Databricks offers powerful compute resources, which are essential for processing large datasets efficiently.
- However, this comes at a significant cost, especially when scaling to handle increased data volumes. I chose a "pay-as-you-go" model to manage this, ensuring that I only incur costs when processing is required, but this necessitates careful job scheduling and monitoring to prevent unexpected expenses. I terminate the clusters when they are not in use.

Cloud Platform Simplicity:
- Integrating Azure Blob Storage and Azure Databricks provides a robust solution, with each service excelling in its role.
- A single cloud ecosystem, keeps all services within Azure, which simplifies integration but potentially limits the flexibility and specific advantages offered by each platform.

Modularity vs. overhead:
- The use of multiple Databricks instances for different tasks (acquisition, cleaning, and transformation) enhances modularity and separation of concerns, making the pipeline easier to manage and scale. However, this modular approach adds overhead in terms of coordination and orchestration between instances.

Redundancy vs. Speed in Data Storage:
- Storing both raw and cleaned data in Azure Blob Storage ensures data integrity and provides a backup in case of processing errors. This redundancy, while offering safety and audit trails, introduces extra storage costs and potential delays in data retrieval. Directly streaming data from raw to transformed formats could reduce storage needs and processing time but would increase the risk if errors occur during transformation.



