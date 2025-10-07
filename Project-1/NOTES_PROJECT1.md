### Azure End-To-End Data Engineering Project (From Scratch!)

* Created Resource Group
* Created Data Lake by enabling hierarchical storage option on azure blob gen2
* Created Azure Data Factory

##### \################################### BRONZE LAYER ##########################################

* Created bronze, silver and gold directory inside containers in Azure Data Lake or storage account
* Inside ADF We first focused on Static data ingestion from GitHub to bronze directory of our storage account
* For that we created Pipeline with "copy data" and created Datasets as well
* First thing to consider is creating Linked service aka. connection from GitHub to ADF and ADF to storage account
* Now lets move to Dynamic Data ingestion pipeline
* For dynamic data ingestion our base url will be same but relative url will be changing due to many number of files
* For that we need to create 3 parameters one for relative url one for folder and 1 for file name which will be inside a json file that is uploaded into the storage account
* We already created "Copy Data" Activity and used dynamic parameters, uploaded json file on storage account and using "loockup" activity along with "for each" activity is al so created

##### \################################### SILVER LAYER ###########################################

* Now on our resource group we created another resource named "Databricks"
* Inside Databrick we created Compute First
* After that we learned about Service Principle and implemented it by creating application from entra id on azure
* Use these credentials to connect blob storage with Databricks

&nbsp;	application id: 11ad1b81-1cf6-4f98-a1ce-1fe35239f026

&nbsp;	tenant id: ada06c13-fb56-4ea0-a5f9-5ba91a475d42

&nbsp;	value: ULx8Q~NfA-BYWPQPyHCqQAv70DexIIi6K4\_kjcHM

* Now that we have connected databricks with blob storage to access bronze layer storage
* We can now acess all those csv files in a dataframe here on databricks
* NOw the next step is doing transformations 
* After transformations are done we save all those transformed data into a silver layer within our data lake

##### \################################### GOLD LAYER  ############################################

* now we addd another resource called synapse analytics where we can create sql workspace and serverless databases.
* Now in order to fetch data from silver layer we use something called openrowset(). basically a powerful function or an abstraction layer that is used to fetch data from data lake but in a tabular foemat like we fetch from SQL table but here in a data lake so often called lake house.
* Then we created views and then fetched all those data from silver layer inside view now we can directly query views
* Now WE create extrenal tables by transferring data from silver layer to gold with the help of CETAS
* FINALLY WE SERVE THE DATA ON POWER BI.







