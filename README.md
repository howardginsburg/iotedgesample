# IoT Edge 1.2 Sample Solution

This project is meant to kickstart an IoT Edge 1.2 project using VSCode.  It leverages the sample temperature sensor module, and then adds a basic logging module as well as the IoT Edge Monitor module.  

## Requirements

1. IoT Hub - [Instructions](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-through-portal?view=iotedge-2020-11#create-an-iot-hub)
2. Ubuntu VM with IoT Edge installed - [Instructions](https://docs.microsoft.com/azure/iot-edge/how-to-provision-single-device-linux-symmetric?view=iotedge-2020-11&tabs=azure-portal%2Cubuntu)
3. Azure Container Registry - [Instructions](https://docs.microsoft.com/Azure/container-registry/container-registry-get-started-portal#create-a-container-registry)
4. Log Analytics Workspace - [Instructions](https://docs.microsoft.com/en-us/azure/azure-monitor/logs/quick-create-workspace)
5. Visual Studio Code - [Download Page](https://code.visualstudio.com/) and [Azure IoT Tools Extension Page](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-tools)

## Deployment

1. Download this repo as a zip file and then unzip to a new directory.
2. Rename .envsample to .env and enter the required data points.
3. From the terminal command line, connect to your azure container registry using `az acr login --name <registry name>`.
4. Right click on deployment.template.json and select 'Build and Push IoT Edge Solution'.  This will build containers for all the modules and push them to your azure container registry.
5. Right click on deployment.template.json and select 'IoT Edge Deployment Manifest'.  This will create a deployment file for the AMD64 platform in the config directory.
7. Right click on deployment.amd64.json and select 'Create Deployment for Single Device' and then select your iot edge.

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