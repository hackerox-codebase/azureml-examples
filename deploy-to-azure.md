## Create an Azure ML workspace in the subscription
- https://learn.microsoft.com/en-us/azure/machine-learning/quickstart-create-resources?view=azureml-api-2

## Deploy and score a machine learning model by using an online endpoint
- https://learn.microsoft.com/en-us/azure/machine-learning/how-to-deploy-online-endpoints?view=azureml-api-2&tabs=azure-cli
- Commands to register a model and create an endpoint with a deployment
    - az account set -s "e991f3b9-590e-41e8-95d1-332f39d437b4"
        - Our subscription id.
    - az configure --defaults group=Development workspace=AMLWorkspace
    - az ml online-endpoint create --local -n my-endpoint -f endpoints/online/managed/sample/endpoint.yml
    - az ml online-deployment create --local -n blue --endpoint my-endpoint -f endpoints/online/managed/sample/blue-deployment-updated.yml
    - az ml online-endpoint show -n my-endpoint --local
    - az ml online-deployment get-logs --local -n blue --endpoint my-endpoint
    - az ml online-endpoint invoke --local --name my-endpoint --request-file endpoints/online/model-1/sample-request.json
    - az ml online-endpoint show -n my-endpoint  --query traffic
        - Shows which deployment receives how much traffic.
     
    Note: Run the commands without --local, once you can test the deployment on your local docker engine.

  ## Sample request
  Request URL: 'https://my-endpoint.centralindia.inference.ml.azure.com/score'\
  Request method: 'POST'\
  Request headers:\
      &emsp;'Content-Type': 'application/json'\
      &emsp;'Content-Length': '76'\
      &emsp;'Authorization': 'Bearer HbuRkID3dTRWVHlakAjIRxUwmsxPvsi1'\
      &emsp;'azureml-model-deployment': 'blue'\
  Request body:\
  {"data": [[1, 2, 3, 4, 5, 6, 7, 8, 9, 10], [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]]}
