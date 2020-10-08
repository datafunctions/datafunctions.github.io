# Python package (dfio)
We use and maintain a python package on PyPi called `dfio`.  

In order to use any of the modules and functions, simply pip install in your working (preferably virtual) environment:

`pip install dfio`

These functions are designed to be used in deployed Cloud Functions, so appropriate permissions should be attached to the associated service account used for execution.  

## Environment Variables (local environment)
Local execution and testing will require setting the following environment variables in your IDE:

=== "GCP_PROJECT"
    ```
    Description: Current project_id
    ```
    
=== "GOOGLE_APPLICATION_CREDENTIALS"
    ```
    Description: Relative path to credentials JSON file with appropriate permissions
    ```
 
## dfio.utilities
Utility functions:
### get_local_json_file_as_dict


 
## dfio.gcs
Functions for interacting with Google Cloud Storage

### upload_url_to_gcs

## dfio.testing
Functions for seamless local testing of Cloud Functions

### execute_local_cf_test_with_pubsub_payload






## Configurations
In the terminal: `pip install dfconfig`


## Google Cloud Storage

In the terminal: `pip install dfgcs`
