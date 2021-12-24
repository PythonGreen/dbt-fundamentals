Welcome to your new dbt project!

### Using the starter project

Try running the following commands:
- dbt run
- dbt test


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
