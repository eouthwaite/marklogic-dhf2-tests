# marklogic-dhf2-tests

Example for using marklogic-unit-tests with data-hub-framework 1 or 2 - for later versions, follow the [example projects](https://github.com/marklogic/marklogic-data-hub)

## How it works

This is not a pretty work-around.

    gradle myDeploy

If the environment is not in the list on line 145, **mlDeploy** is invoked; otherwise **deployTest** is run:

- **copyTestDBConfig** - copies unit test database config from `src/test/ml-config/databases` prior to deployment
- **copyTestEPConfig** - copies unit test end point config from `src/test/ml-config/servers` prior to deployment
- **copyUnitTestModules** - copies unit test scaffolding files from `build/mlRestApi/marklogic-unit-test-modules/ml-modules/root` prior to deployment
- **mlDeploy** - normal data-hub deployment
- **deployTestData** - Deploys the `/src/test/ml-modules/root/test` directory into the Modules DB without corrupting binaries (this is a workaround for a DHF1 and 2 issue which will affect test data containing PDFs, images etc)
- **removeMLUnitTest** - removes unit test scaffolding files copied by copyUnitTestModules
- **removeTestDBConfig** - removes unit test database config copied by copyTestDBConfig
- **removeTestEPConfig** - removes unit test end point config copied by copyTestEPConfig
