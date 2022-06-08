# IoT Edge 1.2 Sample Solution

This project is meant to kickstart an IoT Edge 1.2 project using VSCode.  It is meant to stitch together several module patterns so the developer can decide what makes the most sense for them.  The general architecture is:

Simulated Temperature Sensor Module -> C# Module -> Azure Function Module -> Stream Analytics Edge Module -> IoT Hub.

## Requirements

1. IoT Hub - [Instructions](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal?view=iotedge-2020-11#create-an-iot-hub)
2. Ubuntu VM with IoT Edge installed - [Instructions](https://docs.microsoft.com/azure/iot-edge/how-to-provision-single-device-linux-symmetric?view=iotedge-2020-11&tabs=azure-portal%2Cubuntu)
3. Azure Container Registry - [Instructions](https://docs.microsoft.com/Azure/container-registry/container-registry-get-started-portal#create-a-container-registry)
4. Log Analytics Workspace - [Instructions](https://docs.microsoft.com/azure/azure-monitor/logs/quick-create-workspace)
5. Azure Storage - [Instructions](https://docs.microsoft.com/azure/storage/common/storage-account-create?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&tabs=azure-portal)
    - The default values are fine.
6. Stream Analytics Workspace for Edge - [Instructions](https://docs.microsoft.com/azure/iot-edge/tutorial-deploy-stream-analytics?view=iotedge-2020-11)
    - Complete up through Create a New Job.
7. Visual Studio Code - [Download Page](https://code.visualstudio.com/) and [Azure IoT Tools Extension Page](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-tools)

## Deployment

1. In the Azure portal, navigate to your Steam Analytics resource.
2. Select the Storage Account Settings blade and select the storage account resource you created.
3. Select the Inputs blade and create a new edgeHub input named "edgehubinput" and then save.
4. Select the Outputs blade and create a new edgeHub output named "edgehuboutput" and then save.
5. Select the Query blade and paste the following basic query: `SELECT * INTO [edgehuboutput] FROM [edgehubinput]`
6. Select the Publish blade and publish the job definition.  Make note the the Job Info token.
7. Download this repo as a zip file and then unzip to a new directory.
8. Rename .envsample to .env and enter the required data points.
9. From the terminal command line, connect to your azure container registry using `az acr login --name <registry name>`.
10. Right click on deployment.template.json and select 'Build and Push IoT Edge Solution'.  This will build containers for all the modules and push them to your azure container registry.
11. Right click on deployment.template.json and select 'IoT Edge Deployment Manifest'.  This will create a deployment file for the AMD64 platform in the config directory.
12. Right click on deployment.amd64.json and select 'Create Deployment for Single Device' and then select your iot edge.  Alternatively, you can also run the sample within the simulator in vscode.

## Evaluating Results

### IoT Edge

1. Log into your iot edge box.
2. View the running modules using `sudo iotedge list`
3. View the logs of each module using `sudo iotedge logs <module name>`

### IoT Edge Metrics Collector

1. In the Azure Portal, navigate to your IoT Hub resource.
2. Select the 'Workbooks' blade under 'Monitoring'
3. Explore the different IoT Edge workbooks.

### Defender for IoT

1. In the Azure Portal, navigate to your IoT Hub resource.
2. Select the 'Overview' blade under 'Defender for IoT'.
3. Explore the different options and alerts.