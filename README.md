# Data-Analytics-Week-3
# DATA QUALITY CHALLANGES
- Analysts often analyze data in data warehouses, but each source has unique quality issues that need resolution.
- Before analyzing, analysts must examine each data source and resolve any underlying issues, such as cleaning and profiling datasets for various reasons.

_Duplicate Data:_
- Duplicate data occurs when data from the same transaction is accidentally duplicated within a system.
- This can occur when users double-click on a file or when multiple data sources for the same data elements are used.
- System architects work to prevent duplicate data creation by implementing visual warnings to alert users.
- To resolve duplicate data issues, companies have a duplicate resolution process that checks for customers with multiple billing addresses, validates the correct address, and updates the Sales database by removing the duplicate record.
- This helps prevent the creation of duplicate data and ensures accurate and efficient system operations.

_Redundant Data:_
- Data redundancy occurs when the same data elements exist in multiple places within a system, often due to integrating multiple systems.
- This is because shared data elements in different systems can cause conflicting values across systems.
- For example, a Sales ETL Job copies data from the Sales database into the Warehouse, while the Accounting ETL Job copies accounting data into the Warehouse.
- This creates a potential data redundancy problem, as different systems have different addresses for the same customer.
- Resolving redundant data involves synchronizing changes to shared data elements between the Accounting and Sales systems, but technical or political realities can make this impossible.
- The integrated ETL process uses a delta load approach to update addresses and ensure correct warehouse values.
- This helps resolve data discrepancies between Sales and Accounting systems.
- Inappropriate database design, such as billing by the hour, can also cause data redundancy.

_Missing Values:_
- Missing values, also known as null values, are issues that affect data quality.
- Null values are the absence of a value, not a space or blank. While some situations allow for null values, such as in a Middle Initial column, they can pose calculation challenges.
- For example, a temperature sensor's temperature column might have a null value for January 4, 2020, causing an error. Null values can be problematic depending on the data analysis tools used. SQL offers functions to check for null values and replace them with a user-specified value, while Python and R offer similar functions.

_Invalid Data:_
- Invalid data refers to values outside the valid range for a given attribute, violating business rules rather than having incorrect data types.
- Understanding the context of a system is crucial to determine if a value is invalid.
- For example, a temperature sensor with a date data type and a numeric temperature column is invalid if it is an unrealistic number.
- Programming languages lack native functions to determine invalid values, so data professionals must work with software developers to create rules based on their organization's unique needs.
- Invalid values violate business rules, not technical ones.
- Data professionals should work with software developers to create rules based on their organization's unique needs.
- Numeric and date data are easier to check for invalid values, while text data is more complex and can be invalid due to lack of referential integrity.

_Nonparametric Data:_
- Nonparametric data is collected from categorical variables, which can indicate differentiation or rank order.
- The rank order of the values is of significance, not the individual values themselves.
- For example, a person with abdominal pain may rate their pain on a scale of 0 to 10, which helps put their discomfort in context.
- If the person answers 8 on the scale, it equates to severe pain, and the doctor might order an X-ray or ultrasound to inform treatment options.

_Data Outliers:_
- A data outlier is a value that significantly differs from other observations in a dataset.
- For example, in a real estate sale price example, the property at 130 Main Street has a sale price of $26,496,400, which is significantly higher than the rest.
- Understanding outliers is crucial for analyzing data.
-  For example, if the property is a commercial property, it should be removed from the dataset for residential real estate prices analysis. If it's not a commercial property, a data entry error may have created the outlier, requiring correction. Outliers exist regardless of data type.

_Specification Mismatch:_
- A specification is a document that outlines the target value for a component, and a specification mismatch occurs when an individual component's characteristics are beyond acceptable values.
- For example, if a wooden stud is purchased with a rectangular cross-section, it may not match the blueprint. To avoid complications, the board is replaced with a 2x4. In manufacturing, a specification mismatch can cause a component to fail post-production quality checks.
- Understanding a specification's tolerance is crucial for maintaining quality. Invalid data has values that fall outside a given range.
- A specification mismatch can also occur when data does not conform to its destination data type.
- To resolve this mismatch, it is necessary to validate that the inbound data consistently maps to its target data type.

_Data Type Validation:_
- Data type validation ensures consistent data types in datasets.
- The load process handles data type validation failures, affecting the successful loading of remaining rows.
- Programming languages like SQL, Python, and R have data type validation functions.
- Detecting and resolving issues early is crucial for data readiness for analysis.
- Depending on the tool, a single failure may cause the process to stop or write each failed record to an error file.

# Data Manipulation Techniques
- This section discusses various potential data quality issues and discusses various data manipulation techniques to address these concerns.

_Recoding Data:_
- Recoding data is a method that maps original values of a variable into new ones for analysis.
- It groups data into multiple categories, creating a categorical variable. Categorical variables can be nominal or ordinal, with no natural order or inherent rank. Recoding is useful when analyzing numeric data by category.
- For example, if a hospital administrator needs to determine the number of people reporting moderate pain according to a pain scale, they can recode the numeric data and create a categorical variable.
- This process can be implemented regardless of the programming language used. The Pain_Category column is created, and the administrator can now understand that two people reported moderate pain.

_Derived Variables:_
- A derived variable is a new variable created from a calculation on an existing variable.
- It can be categorical or not.
- For example, a patient's age is a function of the current date, not the date of birth. To avoid potential age-related data errors, it is better to embed the formula to derive age in code, ensuring the value is obtained exactly when needed, rather than keeping it as a derived column.

_Data Merge:_
- A data merge is a process that combines multiple datasets with different structures into a single dataset, improving data quality by adding new variables.
- This process is commonly used in Enterprise Resource Planning (ERP) processes to transform data for analytical environments.
- By adding columns to a dataset, merging provides additional data about a specific observation.
- For example, to obtain an overall picture of a person's health, one might merge records from their primary care physician, self-reported dietary and exercise habits, and other sources of data.
- This would result in a table with additional columns, augmenting the amount of data about each person in the population. This data append is part of the ETL process, facilitating advanced analytical techniques.

_Data Blending:_
- Data blending is a process that combines multiple data sources into a single dataset at the reporting layer.
- It differs from Extract, Transform, and Load (ETL) in that it allows analysts to combine datasets ad hoc without saving them in a relational database.
- The blended dataset exists only at the reporting layer, not in the source databases.
- Data visualization tools like Tableau allow analysts to connect to different source systems and blend the data using a shared attribute.
- Data blending can reduce IT burdens by allowing analysts to merge data. However, the level of knowledge required for productivity is crucial.
- ETL processes are programmatic and operate on a schedule, resulting in a merged dataset that persists at the data layer.
- Data blending connects data at the visualization layer, allowing analysts to integrate additional data sources in an ad hoc, exploratory manner.

_Concatention:_
- Concatenation is the merging of separate variables into a single variable, which is useful in dealing with source systems that store components of a single variable in multiple columns.
- It is particularly useful when dealing with date and time data, generating address information, or aggregating temperature sensor data for analysis tools.
- Programming languages like SQL, Python, and R have functions that make concatenation easy, making it a straightforward activity to combine data in various applications.

_Data Append:_
- A data append is a process where multiple data sources with the same structure are combined to create a new dataset.
- This process is used for ongoing analysis, such as in meteorology or franchising.
- The National Weather Service (NWS) provides data from multiple weather stations, which are then appended by the NWS server. This data is then used to base forecasts.
- For example, a franchisor with multiple franchisee locations can use the same point of sales system to aggregate sales analysis, appending data from each franchise into a single table for ongoing analysis.

_Imputation:_
- Imputation is a technique used to replace missing values in data from multiple sources, such as sensor data.
- It can be caused by various reasons, such as lost network connections, manual scale use, or inability to record values. To handle missing data, analysts can use various approaches:
      - Remove Missing Data: This method removes rows with missing values without       affecting the overall analysis. Replace with Zero: This method replaces           missing values with a zero, which is not appropriate as a person's weight         should be a positive number.
      - Replace with Overall Average: This method computes the average weight             value for all rows with data and replaces missing values with that.
      - Replace with Most Frequent (Mode): This method uses the most frequently           occurring value as a constant.
      - Closest Value Average: This method uses the values from the rows before           and after missing values, like 2/13/2021 and 2/14/2021.

_Reduction:_
- Reduction is a method used to shrink a large dataset without affecting its analytical value.
- There are various techniques available, including dimensionality and numerosity reduction, depending on the type of data and the analysis objectives.
- These techniques are often inefficient and unfeasible when dealing with big data.

_Dimensionality Reduction:_
- Dimensionality reduction is a technique that reduces the size of a dataset by removing attributes.

_Numerosity Reduction:_
- Numerosity reduction is a technique that reduces the overall volume of data, especially when dealing with large datasets.
- For example, a decade's worth of Weight Log data can represent 3,650 individual data points per person, which can be overwhelming for a laptop or desktop. To improve efficiency, numerosity reduction can be used.
- Creating a histogram, a diagram made up of rectangles or bars, can help reduce the volume of quantitative data. Histograms can be created in Python, R, and visualization-specific tools, and can be used to represent a range of values.
- Regardless of the number of data points, both histograms convey the number of times each weight occurs in the data.
- Sampling is another approach to reducing data, selecting a subset of individual records from the initial dataset.
- The most straightforward technique is a random sample, which can be used in many cases.
- The time to produce these diagrams varies, with a standard laptop processing the entire dataset in about 45 seconds, while creating a sample-based histogram takes only 0.2 seconds.
- Sampling is a common approach for improving analyst efficiency as data volumes increase:
              1.Aggregation: Data aggregation is the summarization of raw data for analysis.
              2. Transposition: Transposing data is when you want to turn rows into columns or columns into rows to facilitate analysis
              3. Normalization: Normalizing data differs from our discussion of database normalization
              4. Min-Max Normalization
              5. Parsing/String Manipulation


# Managing Data Quality
- To enhance data quality, analysts must identify scenarios that trigger issues and create a mental checklist by exploring different situations and examining the application of different data quality controls.

_Circumstances to Check for Quality:_
- Implementing data quality control checks is crucial throughout the data life-cycle journey, as errors during acquisition, transformation, manipulation, and visualization can degrade data quality.
- Recognizing potential quality issues and having a comprehensive strategy is essential for ensuring data quality.
- We ensure it the following:
            1. Data Acquisiton
            2. Data Transformation and Conversion
            3. Data Manipulation
            4. Final Product Preparation

_Aumotated Validation:_
- Analytics environments often rely on various data sources, including computer systems and human-generated ones.
- Data entry mistakes can negatively impact data quality, so automating data validation checks can help.
- Understanding how source data fields map to their corresponding database columns is crucial.
- Paying attention to data types in the database can prevent errors.
- For instance, if a web form allows free text entry, automating data type validation before passing data to the database can prevent data type mismatches.
- Similarly, verifying the number of data points can help identify sensor failures early, preventing missing data from flowing into the analytics environment.
- Automating these checks can help maintain data quality and prevent data entry errors.

_Data Quality Dimensions:_
- To improve data quality, it's crucial to consider six dimensions: accuracy, completeness, consistency, timeliness, uniqueness, and validity.
- Understanding these dimensions and their relationships can enhance data quality, thereby enhancing overall data quality.
- These are each dimensions:
            1. Data Accuracy
            2. Data Completeness
            3. Data Consistency
            4. Data Timeliness
            5. Data Uniqueness
            6. Data Validity

_Data Quality Rules and Metrics:_
- Data quality dimensions, including data conformity, accuracy, consistency, uniqueness, and validity, are crucial for improving overall quality. Nonconformity occurs when source data does not match the destination data type size and format.
- For instance, the Warehouse Load ETL (ETL) job needs to ensure consistency when propagating data from different source systems into the Data Warehouse.
- Nonconformity can be addressed by confirming the number of successful rows and the number of failed rows.
- For example, if a customer has an 11-character last name, the ETL job needs to copy the bill details but not the last name field when loading the Data Warehouse.
- This creates a data quality issue in the Data Warehouse.
- To validate data conformity issues, confirm the number of successful rows and the number of failed rows.
- For example, if 900,000 rows are successful, the Warehouse Load ETL job sends 100,000 nonconforming rows to a Bad Data staging area.
- A data engineer resolves the root cause of the data quality issue before sending the remediated data into the Data Warehouse. This approach makes efficient use of resources and improves quality.

_Methods to Validate Quality:_
- Various methods are available to validate data quality, including assessing data accuracy and identifying irregular patterns.
- A effective approach is to combine these methods effectively.
- Reasonable Expections: To ensure data quality in your analytics environment, it's crucial to assess if the data meets your reasonable expectations. For instance, if your transactional systems process 10 million records daily, you should expect 300 million records by 30 days. If only 20 million are seen, it's likely that the data propagation ETL is failing. To automate this, create exception reports in your ETL processes. If successful rows are less than attempted rows, internal alarms should be raised, and the root cause of the ETL load failure should be addressed.
- Data Profiling: Data profiling is a method to enhance data quality by identifying discrepancies, irregular patterns, and missing values. It can help analyze customer engagement by examining the frequency of customer logins. For instance, a customer might log in three hundred times per day from three hundred unique devices, originating from multiple locations. This data fails the reasonable expectation test, as customers typically log in less frequently and from fewer devices. Therefore, it's crucial to investigate the data's authenticity rather than trusting it.
- Data Audits: Data audits are crucial for businesses to ensure they have the necessary data for operations. They use data profiling techniques to identify data integrity and security issues. For instance, a large company with numerous suppliers may discover a large payment was sent to a new financial institution, leading to a fraud investigation. The company should develop a security awareness program to help employees recognize fraudulent transfers.
- Sampling: Sampling is a statistical technique used to validate data quality by examining a sample of data. For instance, in an automotive manufacturer, assessing the quality of fasteners is not cost-effective due to the high production volume. Instead, a sample from each shipment is evaluated against the specifications for that fastener. This approach is best done in partnership with a statistician. In a streaming media company, assessing the quality of each movie transmitted across a network connection is cost-effective.
- Cross-Validation: Cross-validation is a statistical technique used by analysts to evaluate the performance of predictive models. It divides data into two subsets: the training set and the testing set. The model is built using the training data and cross-validated to determine its accuracy. Cross-validation helps identify data sampling issues, such as sampling bias, which can lead to inaccurate predictions.
