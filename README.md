Welcome to your new dbt project!

### Using the starter project

Try running the following commands:
- dbt run
- dbt test

## Naming Conventions 

In working on this project, we established some conventions for naming our models.

- **Sources** (src) refer to the raw table data that have been built in the warehouse through a loading process. (We will cover configuring Sources in the Sources module)
- **Staging** (stg) refers to models that are built directly on top of sources. These have a one-to-one relationship with sources tables. These are used for very light transformations that shape the data into what you want it to be. These models are used to clean and standardize the data before transforming data downstream. Note: These are typically materialized as views.
- **Intermediate** (int) refers to any models that exist between final fact and dimension tables. These should be built on staging models rather than directly on sources to leverage the data cleaning that was done in staging.
- **Fact** (fct) refers to any data that represents something that occurred or is occurring. Examples include sessions, transactions, orders, stories, votes. These are typically skinny, long tables.
- **Dimension** (dim) refers to data that represents a person, place or thing. Examples include customers, products, candidates, buildings, employees.
- Note: The Fact and Dimension convention is based on previous normalized modeling techniques.

## Reorganize Project

- When dbt run is executed, dbt will automatically run every model in the models directory.
- The subfolder structure within the models directory can be leveraged for organizing the project as the data team sees fit.
- This can then be leveraged to select certain folders with dbt run and the model selector.
- Example: If dbt run -s staging will run all models that exist in models/staging. (Note: This can also be applied for dbt test as well which will be covered later.)
- The following framework can be a starting part for designing your own model organization:
- **Marts** folder: All intermediate, fact, and dimension models can be stored here. Further subfolders can be used to separate data by business function (e.g. marketing, finance)
- **Staging** folder: All staging models and source configurations can be stored here. Further subfolders can be used to separate data by data source (e.g. Stripe, Segment, Salesforce). (We will cover configuring Sources in the Sources module)

## Sources

- Sources represent the raw data that is loaded into the data warehouse.
- We can reference tables in our models with an explicit table name (raw.jaffle_shop.customers).
- However, setting up Sources in dbt and referring to them with the source function enables a few important tools.
    - Multiple tables from a single sources can be configured in one place.
    - Sources are easily identified as green nodes in the Lineage Graph.
    - You can use dbt source freshness to check the freshness of raw tables.

## Configuring sources

- Sources are configured in YML files in the models directory.
- View the full documentation for configuring sources on the source properties page of the docs.
- The ref function is used to build dependencies between models.
- Similarly, the source function is used to build the dependency of one model to a source.

## Source freshness

- Freshness thresholds can be set in the YML file where sources are configured. For each table, the keys loaded_at_field and freshness must be configured
- A threshold can be configured for giving a warning and an error with the keys warn_after and error_after.
- The freshness of sources can then be determine with the command dbt source freshness.

## Tests in dbt

* In dbt, there are two types of tests - schema tests and data tests:
    - **Generic tests** are written in YAML and return the number of records that do not meet your assertions. These are run on specific columns in a model.
    - **Specific tests** are specific queries that you run against your models. These are run on the entire model.
* dbt ships with four built in tests: unique, not null, accepted values, relationships.
    - **Unique** tests to see if every value in a column is unique
    - **Not_null** tests to see if every value in a column is not null
    - **Accepted_values** tests to make sure every value in a column is equal to a value in a provided list
    - **Relationships** tests to ensure that every value in a column exists in a column in another model (see: referential integrity)
* Generic tests are configured in a YAML file, whereas specific tests are stored as select statements in the tests folder.
* Tests can be run against your current project using a range of commands:
    - dbt test runs all tests in the dbt project
    - dbt test --select test_type:generic
    - dbt test --select test_type:singular
    - dbt test --select one_specific_model
* Read more here in [testing documentation](https://docs.getdbt.com/reference/node-selection/test-selection-examples)
* In development, dbt Cloud will provide a visual for your test results. Each test produces a log that you can view to investigate the test results further



### Resources:
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [dbt community](http://community.getbdt.com/) to learn from other analytics engineers
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices
