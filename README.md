# Dapr Workflow Retail Demo

Demo of the Dapr Workflow building block in a retail context.

## Run the Workflow App

1. Change to the Retail directory and build the ASP.NET app:

    ```bash
    cd Retail
    dotnet build
    ```

2. Run the app using the Dapr CLI:

    ```bash
    dapr run --app-id order-processor --app-port 5064 --dapr-http-port 3500 --resources-path ./Resources dotnet run
    ```

    > Ensure the --app-port is the same as the port specified in the launchSettings.json file.

3. Restock the inventory:

    ```bash
    curl -X GET http://localhost:5064/stock/restock
    ```

4. Start the workflow:

   ```bash
   curl -i -X POST http://localhost:3500/v1.0-alpha1/workflows/dapr/OrderProcessingWorkflow/1234/start \
     -H "Content-Type: application/json" \
     -d '{ "input" : {"Name": "Paperclips", "TotalCost": 99.95, "Quantity": 1}}'

5. Check the workflow status:

    ```bash
    curl -i -X GET http://localhost:3500/v1.0-alpha1/workflows/dapr/OrderProcessingWorkflow/1234/status
    ```
