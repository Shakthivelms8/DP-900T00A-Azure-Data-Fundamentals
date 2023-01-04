# Provision Azure relational database services

As part of your role at Contoso as a data engineer, you've been asked to create and configure SQL Server, PostgreSQL, and MySQL servers for Azure.

Select a region from the following list when you create resources:

-   West US 2
-   South Central US
-   Central US
-   East US
-   West Europe
-   Southeast Asia
-   Japan East
-   Brazil South
-   Australia Southeast
-   Central India

## Task 1: Create your Azure SQL Database service

In this task you'll set up your Azure SQL Database instance, which includes creating your server.

Over time if you realize you need additional compute power to keep up with demand, you can adjust performance options or even switch between the DTU and vCore performance models.

1.  Open **Edge Browser** and log in to the **Azure portal**. When prompted, use the credentials provided within the **Environment Details** tab of the lab guide.

    ![Environment details](media/environment-details.png "Environment details")
    

    >**NOTE**- The DeploymentID can be obtained from the Lab Environment output page.

2.  In the portal, select **Create a resource** from the upper left-hand corner. Select **Databases**, then select **SQL Database**.

    ![create sql database](media/upd-create-sql-database.png "create sql database")

3.  Enter the following values into the form:

    | Setting | Value  |
    | --- | --- |
    | Subscription | **Default Subscription** |
    | Resource group | **DP900-DID** |
    | Database name | **ContosoDID**, where **DID** is the DeploymentID can be obtained from the Lab Environment output page. |
    | Want to use SQL elastic pool? | **No** |

4.  Under Server, select **Create new**, fill out the Create SQL Database Server form with the following values, and then select **OK**:

    | Setting | Value  |
    | --- | --- |
    | Server name | **sqlDID**, where **DID** is the DeploymentID can be obtained from the Lab Environment output page.|
    | Authentication method | click on **Use SQL authentication** |
    | Server admin login | **azureadmin** |
    | Password | **Pa55w.rd** |
    | Confirm password | **Pa55w.rd** |
    | Location | **Select the default location** |

    ![create sql database](media/upd-sql-database-create.png "Creating SQl database")
    
    ![new server](media/upd-sql-new-server-create.png "new server")

5.  Under **Compute + storage**, select **Configure database**.

6.  On the Configure page, leave vCores set to **2**, change Data max size to **50 GB**, and then select **Apply**.

    ![Configure](media/upd-configure.png "Configure")

7.  Back on the Create SQL Database page, select **Additional settings** tab from top header.

8.  Use these values to fill out the form.

    | Setting | Value  |
    | --- | --- |
    | Use existing data | **None** |
    | Database Collation | **SQL_Latin1_General_CP1_CI_AS** |
    | Maintenance window | **Default** |

    ![new server](media/upd-sql-database-additionalsetting.png "additional")

9.  Select **Review + Create**, and then select **Create** to create your Azure SQL database.  

## Task 2: Create your Azure Database for PostgreSQL service (Optional)

In this exercise, you'll set up Azure Database for PostgreSQL

1.  On the Azure portal, select **Create a resource** from the upper left-hand corner.

2.  Select **Databases**, then select Azure Database for PostgreSQL.

    ![create postgre database](media/upd-create-postgresql-database.png "create postgre database")

3.  On **Select Azure Database for PostgreSQL deployment option** page, Select **Single Server** from the drop-down menu and then click on **Create**.

    ![select postgre service](media/upd-postgresql-service-select.png "select postgre service")
    
4. If prompted with pop-up of **Consider creating flexible server**, Select **No - Create single server**.

5.  Use these values to start filling out the form.

    | Setting | Value  |
    | --- | --- |
    | Subscription | **Default Subscription** |
    | Resource group | **DP900-DID** |
    
6.  Under Server details, use these values:

    | Setting | Value  |
    | --- | --- |
    | Server name | Enter **postgresqlDID**, where **DID** is the DeploymentID can be obtained from the Lab Environment output page.|
    | Data source | **None** |
    | Location | **Select the default location** |
    | Version | **Keep default setting** |

    ![](media/upd-image-100.png)

7.  Under **Compute + storage**, select **Configure server**.

    ![](media/upd-compute.png)
 
8.  Change **vCore** to **two cores**, increase the **storage** to **160 GB**, set the Backup Retention Period to **14 days**, and then select **OK**.
    
    ![select postgre service](media/postgresql-configure.png "postgre configure")

9.  Back on the Single server page, under Administrator account, specify these values:

    | Setting | Value  |
    | --- | --- |
    | Admin username | **azureadmin** |
    | Password | **Pa55w.rd** |
    | Confirm password | **Pa55w.rd** |
    
    ![admin](media/upd-adminacc.png "admin")

10.  Select **Review + Create**, and then select **Create** to create your Azure PostgreSQL database.

## Task 3: Create your Azure Database for MySQL service (Optional)

In this exercise you'll set up Azure Database for MySQL

1.  On the Azure portal, select **Create a resource** from the upper left-hand corner.

2.  Select **Databases**, then select **Azure Database for MySQL**.

    ![azure database for sql](media/upd-create-azure-database-forsql.png "azure database for sql")

3. You will be presented with the choice of a Single server or Flexible server. Under resource type, select **Single server option** from the drop-down menu and then click on **Create**.

    ![azure database for sql](media/upd-dp90002.png "azure database for sql")

4.  Use these values to fill out the first section of the form.

    | Setting | Value  |
    | --- | --- |
    | Subscription | **Default Subscription** |
    | Resource group | **DP900-DID** |

5.  Under Server details, use these values:

    | Setting | Value  |
    | --- | --- |
    | Server name | Enter **mysqlDID**, where **DID** is the DeploymentID can be obtained from the Lab Environment output page. |
    | Data source | **None** |
    | Location | **Select the default location** |
    | Version | **Keep default setting** |

6.  Under **Compute + storage**, select **configure server**.

    ![mysql create](media/mysql-create.png "mysql create")

7.  On the Pricing tier page, reduce **vCore** to **two cores**, set **Storage** between **160 GB** to **170 GB**, change Backup Retention Period to **14 days**, and then select **apply**.

    ![configure azure database](media/configure-azure-database-mysql.png "configure azure database") 

8.  Back on the Create MySQL server page, under Administrator account, use these values

    | Setting | Value  |
    | --- | --- |
    | Admin username | **azureadmin** |
    | Password | **Pa55w.rd** |
    | Confirm password | **Pa55w.rd** |
    
    ![admin](media/upd-adminacc.png "admin")

9.  Select **Review + Create**, and then select **Create** to create your Azure MySQL database.

## Congratulation, you have completed this lab.
------------