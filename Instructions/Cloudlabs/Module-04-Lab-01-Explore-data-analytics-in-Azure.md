# Explore Azure Synapse Analytics

In this exercise, you'll use the already provisioned Azure Synapse Analytics workspace in your Azure subscription, to ingest and query data.

## Exercise 1 : Explore Azure Synapse Analytics

In this exercise, you'll use the Azure Synapse Analytics workspace to ingest and analyze some data.

The exercise is designed to familiarize you with some key elements of a modern data warehousing solution, not as a comprehensive guide to performing advanced data analysis with Azure Synapse Analytics. 

### Task 1 : Explore an Azure Synapse Analytics workspace

1.  Open the resource group **DP-900-Module-4**  that was precreated for you and notice that it contains your Synapse Analytics workspace, a Data Lake storage account and an Apache Spark pool.
    
7.  Select your Synapse workspace, and in its  **Overview**  page, in  **Open Synapse Studio**  card, select  **Open**  to open Synapse Studio in a new browser tab. Synapse Studio is a web-based interface that you can use to work with your Synapse Analytics workspace.
    
8.  On the left side of Synapse Studio, use the  **››**  icon to expand the menu - this reveals the different pages within Synapse Studio that you'll use to manage resources and perform data analytics tasks, as shown here:
    
    ![Image showing the expanded Synapse Studio menu to manage resources and perform data analytics tasks](media/synapse-studio.png)
    

### Task 2 : Ingest data

One of the key tasks you can perform with Azure Synapse Analytics is to define  _pipelines_  that transfer (and if necessary, transform) data from a wide range of sources into your workspace for analysis.

1.  In Synapse Studio, on the  **Home**  page, select  **Ingest**  and then choose  **Built-in copy task**  to open the  **Copy Data tool**  tool.
    
2.  In the Copy Data tool, on the  **Properties**  step, ensure that  **Built-in copy task**  and  **Run once now**  are selected, and click  **Next >**.
    
3.  On the  **Source**  step, in the  **Dataset**  substep, select the following settings:
    
    -   **Source type**: HTTP
    -   **Connection**:  _Create a new connection with the following properties:_
        -   **Name**: AdventureWorks Products
        -   **Description**: Product list via HTTP
        -   **Connect via integration runtime**: AutoResolveIntegrationRuntime
        -   **Base URL**:  `https://raw.githubusercontent.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/master/Azure-Synapse/products.csv`
        -   **Server Certificate Validation**: Enable
        -   **Authentication type**: Anonymous
4.  After creating the connection, on the  **Source/Dataset**  substep, ensure the following settings are selected, and then select  **Next >**:
    
    -   **Relative URL**:  _Leave blank_
    -   **Request method**: GET
    -   **Additional headers**:  _Leave blank_
    -   **Binary copy**:  Unselected
    -   **Request timeout**:  _Leave blank_
    -   **Max concurrent connections**:  _Leave blank_
5.  On the  **Source**  step, in the  **Configuration**  substep, select  **Preview data**  to see a preview of the product data your pipeline will ingest, then close the preview.
    
6.  After previewing the data, on the  **Source/Configuration**  step, ensure the following settings are selected, and then select  **Next >**:
    
    -   **File format**: DelimitedText
    -   **Column delimiter**: Comma (,)
    -   **Row delimiter**: Line feed (\n)
    -   **First row as header**: Selected
    -   **Compression type**: None
7.  On the  **Target**  step, in the  **Dataset**  substep, select the following settings:
    
    -   **Target type**: Azure Data Lake Storage Gen 2 =  **Connection**:  _Create a new connection with the following properties:_
        -   **Name**: Products
        -   **Description**: Product list
        -   **Connect via integration runtime**: AutoResolveIntegrationRuntime
        -   **Authentication method**: Account key
        -   **Account selection method**: From subscription
            -   **Azure subscription**:  _select your subscription_
            -   **Storage account name**:  _Select your storage account_
        -   **Test connection**: To linked service
8.  After creating the connection, on the  **Target/Dataset**  step, ensure the following settings are selected, and then select  **Next >**:
    
    -   **Folder path**:  _Browse to your file system folder and select **defaultfs**_
    -   **File name**: products.csv
    -   **Copy behavior**: None
    -   **Max concurrent connections**:  _Leave blank_
    -   **Block size (MB)**:  _Leave blank_
9.  On the  **Target**  step, in the  **Configuration**  substep, ensure that the following properties are selected. Then select  **Next >**:
    
    -   **File format**: DelimitedText
    -   **Column delimiter**: Comma (,)
    -   **Row delimiter**: Line feed (\n)
    -   **Add header to file**: Selected
    -   **Compression type**: None
    -   **Max rows per file**:  _Leave blank_
    -   **File name prefix**:  _Leave blank_
10.  On the  **Settings**  step, enter the following settings and then click  **Next >**:

     -   **Task name**: Copy products
     -   **Task description**  Copy products data
     -   **Fault tolerance**:  _Leave blank_
     -   **Enable logging**:  Unselected
     -   **Enable staging**:  Unselected

11.  On the  **Review and finish**  step, on the  **Review**  substep, read the summary and then click  **Next >**.
    
12.  On the  **Deployment**  step, wait for the pipeline to be deployed and then click  **Finish**.
    
13.  In Synapse Studio, select the  **Monitor**  page, and in the  **Pipeline runs**  tab, wait for the  **Copy products**  pipeline to complete with a status of  **Succeeded**  (you can use the  **↻ Refresh**  button on the Pipeline runs page to refresh the status).
    
14.  On the  **Data**  page, select the  **Linked**  tab and expand the  **Azure Data Lake Storage Gen 2**  hierarchy until you see the file storage for your Synapse workspace. Then select the file storage to verify that a file named  **products.csv**  has been copied to this location, as shown here:
    
![Image showing Synapse Studio expanded Azure Data Lake Storage Gen 2 hierarchy with the file storage for your Synapse workspace](media/synapse-storage.png)
    

### Task 3 : Use a SQL pool to analyze data

Now that you've ingested some data into your workspace, you can use Synapse Analytics to query and analyze it. One of the most common ways to query data is to use SQL, and in Synapse Analytics you can use a  _SQL pool_  to run SQL code.

1.  In Synapse Studio, right-click the  **products.csv**  file in the file storage for your Synapse workspace, point to  **New SQL script**, and select  **Select TOP 100 rows**.
    
2.  In the  **SQL Script 1**  pane that opens, review the SQL code that has been generated, which should be similar to this:
    

    
    ```
    -- This is auto-generated code
    SELECT
        TOP 100 *
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0'
        ) AS [result]
    
    ```
    
    This code opens a rowset from the text file you imported and retrieves the first 100 rows of data.
    
3.  In the  **Connect to**  list, ensure  **Built-in**  is selected - this represents the built-in SQL Pool that was created with your workspace.
    
4.  On the toolbar, use the  **▷ Run**  button to run the SQL code, and review the results, which should look similar to this:
    
| C1     | c2 | c3     | c4       | 
| :---        |    :----:   |    :----:     |  ---:       |
| ProductID      | ProductName       | Category   | ListPrice |
| 771   | Mountain-100 Silver, 38        | Mountain Bikes      |  3399.9900   |
| 772   | Mountain-100 Silver, 42        | Mountain Bikes      |  3399.9900   |
| ...   | ...        | ...      |  ...   |
    
5.  Note the results consist of four columns named C1, C2, C3, and C4; and that the first row in the results contains the names of the data fields. To fix this problem, add a HEADER_ROW = TRUE parameters to the OPENROWSET function as shown here (replacing  _datalakexx_  and  _fsxx_  with the names of your data lake storage account and file system), and then rerun the query:
    

    
    ```
    SELECT
        TOP 100 *
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0',
            HEADER_ROW = TRUE
        ) AS [result]
    
    ```
    
    Now the results look like this:

    | ProductID      | ProductName       | Category   | ListPrice |
    | :---        |    :----:   |    :----:     |  ---:       |
    | 771   | Mountain-100 Silver, 38        | Mountain Bikes      |  3399.9900   |
    | 772   | Mountain-100 Silver, 42        | Mountain Bikes      |  3399.9900   |
    | ...   | ...        | ...      |  ...   |
    
    
6.  Modify the query as follows (replacing  _datalakexx_  and  _fsxx_  with the names of your data lake storage account and file system):
    

    
    ```
    SELECT
        Category, COUNT(*) AS ProductCount
    FROM
        OPENROWSET(
            BULK 'https://datalakexx.dfs.core.windows.net/fsxx/products.csv',
            FORMAT = 'CSV',
            PARSER_VERSION='2.0',
            HEADER_ROW = TRUE
        ) AS [result]
    GROUP BY Category;
    
    ```
    
7.  Run the modified query, which should return a resultset that contains the number products in each category, like this:
    
    | Category      | ProductCount      |
    | :---        |  ---:       |
    | Bib Shorts	   | 3        | 
    | Bike Racks	   | 1        | 
    | ...   | ...        | ...      |  ...   |
    
8.  In the  **Properties**  pane for  **SQL Script 1**, change the  **Name**  to  **Count Products by Category**. Then in the toolbar, select  **Publish**  to save the script.
    
9.  Close the  **Count Products by Category**  script pane.
    
10.  In Synapse Studio, select the  **Develop**  page, and notice that your published  **Count Products by Category**  SQL script has been saved there.
    
11.  Select the  **Count Products by Category**  SQL script to reopen it. Then ensure that the script is connected to the  **Built-in**  SQL pool and run it to retrieve the product counts.
    
12.  In the  **Results**  pane, select the  **Chart**  view, and then select the following settings for the chart:
    
     -   **Chart type**: Column
     -   **Category column**: Category
     -   **Legend (series) columns**: ProductCount
     -   **Legend position**: bottom - center
     -   **Legend (series) label**:  _Leave blank_
     -   **Legend (series) minimum value**:  _Leave blank_
     -   **Legend (series) maximum**:  _Leave blank_
     -   **Category label**:  _Leave blank_
    
The resulting chart should resemble this:
    
![Image showing the product count chart view](media/column-chart.png)
    

### Task 4 : Use a Spark pool to analyze data

While SQL is a common language for querying structured datasets, many data analysts find languages like Python useful to explore and prepare data for analysis. In Azure Synapse Analytics, you can run Python (and other) code in a  _Spark pool_; which uses a distributed data processing engine based on Apache Spark.

1.  In Synapse Studio, on the  **Data**  page, browse to the file system for your Synapse workspace. Then right-click  **products.csv**, point to  **New notebook**, and select  **Load to DataFrame**.
    
2.  In the  **Notebook 1**  pane that opens, in the  **Attach to**  list, select the  **spark**  Spark pool to created previously and ensure that the  **Language**  is set to  **PySpark (Python)**.
    
3.  Review the code in the first (and only) cell in the notebook, which should look like this:

    ```
    %%pyspark
    df = spark.read.load('abfss://fsxx@datalakexx.dfs.core.windows.net/products.csv', format='csv'
    ## If header exists uncomment line below
    ##, header=True
    )
    display(df.limit(10))
    
    ```
    
4.  Use the  **▷**  icon to the left of the code cell to run it, and wait for the results. The first time you run a cell in a notebook, the Spark pool is started - so it may take a minute or so to return any results.
    

    > **Note**: 
    If an error occurs because the Python Kernel isn't available yet, run the cell again.

5.  Eventually, the results should appear below the cell, and they should be similar to this:
    
    | c0     | c1 | c2     | c3       | 
    | :---        |    :----:   |    :----:     |  ---:       |
    | ProductID      | ProductName       | Category   | ListPrice |
    | 771   | Mountain-100 Silver, 38        | Mountain Bikes      |  3399.9900   |
    | 772   | Mountain-100 Silver, 42        | Mountain Bikes      |  3399.9900   |
    | ...   | ...        | ...      |  ...   |
    
6.  Uncomment the  _,header=True_  line (because the products.csv file has the column headers in the first line), so your code looks like this:
    
    PythonCopy
    
    ```
    %%pyspark
    df = spark.read.load('abfss://fsxx@datalakexx.dfs.core.windows.net/products.csv', format='csv'
    ## If header exists uncomment line below
    , header=True
    )
    display(df.limit(10))
    
    ```
    
7.  Rerun the cell and verify that the results look like this:
    
    | ProductID      | ProductName       | Category   | ListPrice |
    | :---        |    :----:   |    :----:     |  ---:       |
    | 771   | Mountain-100 Silver, 38        | Mountain Bikes      |  3399.9900   |
    | 772   | Mountain-100 Silver, 42        | Mountain Bikes      |  3399.9900   |
    | ...   | ...        | ...      |  ...   |
    
    Notice that running the cell again takes less time, because the Spark pool is already started.
    
8.  Under the results, use the  **＋ Code**  icon to add a new code cell to the notebook.
    
9.  In the new empty code cell, add the following code:

    ```
    df_counts = df.groupby(df.Category).count()
    display(df_counts)
    ```
    
10.  Run the new code cell by clicking its  **▷**  icon, and review the results, which should look similar to this:

        | Category      | ProductCount      |
        | :---        |  ---:       |
        | Headsets	   | 3        | 
        | Wheels	   | 14        | 
        | ...   | ...        | ...      |  ...   |
    
11.  In the results output for the cell, select the  **Chart**  view. The resulting chart should resemble this:
    
![Image showing category count chart view](media/bar-chart.png)
    
12.  Close the  **Notebook 1**  pane and discard your changes.