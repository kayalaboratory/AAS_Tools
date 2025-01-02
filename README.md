# AAS_Tools
This is the documentation of the referenced tools used in Asset Administration Shell Tool Comparison: A Case Study with Real Digital Twins Used in Petrochemical Industry.

**GitHub repositories of open source implementations can be found below:**

[FA³ST Service](https://github.com/FraunhoferIOSB/FAAAST-Service)

[Eclipse BaSyx™](https://github.com/eclipse-basyx)

[Eclipse AASX Server](https://github.com/eclipse-aaspe/server)

[NOVA Asset Administration Shell](https://gitlab.com/novaas/catalog/nova-school-of-science-and-technology/novaas)


Docker compose files can be achieved from the repositories.

Additionally, our AASX is created with [AASX Package Explorer (v2024-06-10.alpha)](https://github.com/eclipse-aaspe/package-explorer/releases/tag/v2024-06-10.alpha). AASX File can be tested with 3 open sources which are Eclipse BaSyx™, Eclipse AASX Server and FA³ST Service.
AASX Package Explorer (v2024-06-10.alpha) supports only metamodel V3, so created AASX file is not compatible with NOVAAS. For testing NOVAAS, an example AASX file can be created with Metamodel V2 using [aasx-package-explorer.2022-05-10](https://github.com/admin-shell-io/aasx-package-explorer/releases/tag/v2022-05-10). If you want to create your own AASX file to, you can use AASX Package Explorer v2024-06-10.alpha and generated AASX file will be compatible with BaSyx, FA³ST and AASX Server.

## **Uploading the AASX File**

**Eclipse BaSyx**

Eclipse BaSyx has import/export function for AASX or JSON files in the UI (localhost:3000 by default.) Once AASX file imported file will be displayed on dashboard. For other operations endpoints listed as default.

![image](https://github.com/user-attachments/assets/c32f3a25-4e73-428c-b36a-5d43788196e0)


**AASX Server**

Download and export zip file in a folder. Then go to AasxServerBlazor>aasxs directory, add the Industrial_Column_Assets_Merged.aasx inside this folder and run startForDemo.bat or startForDemo.sh. GUI will be hosted on localhost:5001.
```
cd path_to_directory\AasxServerBlazor
AasxServerBlazor.exe --no-security --data-path aasxs --external-blazor http://localhost:5001
```


**FA³ST Service**

Download the jar file , then run this command in  CLI
```
java -jar starter-{version}.jar --model path_to_directory\Industrial_Column_Assets_Merged.aasx --no-validation
```

### API Documentation

Open source implementations are using Open API integration, entire API Collection can be found at [SwaggerHub](https://app.swaggerhub.com/apis/Plattform_i40/Entire-API-Collection/V3.0.1)

To reach endpoint you need to run these commands. For example, asset administration shells can be received via GET command. If you run files in AASX server base address will be localhost:5001 by default so this command will return AASs.
```
curl -X GET localhost:5001/shells
```
Result
```json
{"result":[{"idShort":"RecoveryAbsorberAAS","id":"https://admin-shell.io/idta/aas/DigitalNameplate/2/0","assetInformation":{"assetKind":"Type","globalAssetId":"https://admin-shell.io/idta/asset/DigitalNameplate/2/0","assetType":"Type"},"submodels":[{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/idta/SubmodelTemplate/DigitalNameplate/2/0"}]},{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/ZVEI/TechnicalData/Submodel/1/2"}]},{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/idta/SubmodelTemplate/TimeSeries/1/1"}]}],"modelType":"AssetAdministrationShell"},{"idShort":"RecoveryStripperAAS","id":"https://admin-shell.io/idta/aas/DigitalNameplate/2/0","assetInformation":{"assetKind":"Type","globalAssetId":"https://admin-shell.io/idta/asset/DigitalNameplate/2/0","assetType":"Type"},"submodels":[{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/idta/SubmodelTemplate/DigitalNameplate/2/0"}]},{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/ZVEI/TechnicalData/Submodel/1/2"}]},{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/idta/SubmodelTemplate/TimeSeries/1/1"}]}],"modelType":"AssetAdministrationShell"}],"paging_metadata":{}}
```

![image](https://github.com/user-attachments/assets/d6a0bb50-ca52-4f47-8ee6-2f4951019bce)

For getting specific Asset Administration Shell /shells/{aasIdentifier} command returns a specific Asset Administration Shell. {aasIdentifier} variable is the UTF8-BASE64-URL-encoded string of the AAS's unique ID. In this case it will be:

id":"https://admin-shell.io/idta/aas/DigitalNameplate/2/0"  =>  "aHR0cHM6Ly9hZG1pbi1zaGVsbC5pby9pZHRhL2Fhcy9EaWdpdGFsTmFtZXBsYXRlLzIvMA==", so this command wil return the RecoveryAbsorberAAS:
```
curl -X GET localhost:5001/shells/aHR0cHM6Ly9hZG1pbi1zaGVsbC5pby9pZHRhL2Fhcy9EaWdpdGFsTmFtZXBsYXRlLzIvMA==
```
Result
```json
{"idShort":"RecoveryAbsorberAAS","id":"https://admin-shell.io/idta/aas/DigitalNameplate/2/0","assetInformation":{"assetKind":"Type","globalAssetId":"https://admin-shell.io/idta/asset/DigitalNameplate/2/0","assetType":"Type"},"submodels":[{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/idta/SubmodelTemplate/DigitalNameplate/2/0"}]},{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/ZVEI/TechnicalData/Submodel/1/2"}]},{"type":"ModelReference","keys":[{"type":"Submodel","value":"https://admin-shell.io/idta/SubmodelTemplate/TimeSeries/1/1"}]}],"modelType":"AssetAdministrationShell"}
```
Same method can be used for other open sources by following their Open API documentation.

## Usage of Eclipse BaSyx

Once AASX file uploaded list of endpoints can be used as described by default.

![image](https://github.com/user-attachments/assets/2e39d891-f9b1-4209-a8be-317c35d5ddfd)

Data is read  according to sensor id and type tags and transferred to MQTT node in time flow order. Here, Telegraf application accessing MQTT node sends data to influx database synchronously with config file (token id - org id etc.) it contains. When API request is sent with appropriate time interval for data stored with time tag, determined sensor values can be obtained as query. This process is performed automatically in Eclipse Basyx application via aasx files. Semantic ids seen in Package Explorer screenshot are parsed via Basyx backend and extracted information can be monitored simultaneously on Basyx AAS UI side. 
The data cannot be shared due to privacy reasons, but we will follow a different path to use the AASX file in this repo. Below you can find the topics that Telegraf will be subscribed to. By publishing data via MQTT node in these topics you can display it in BaSyx.
```
topics = [
    "RecyclingAbsorber/ReboilerTemperature",
    "RecyclingAbsorber/ReboilerFlow",
    "RecyclingAbsorber/LeanWaterRecyclepH",
    "RecyclingAbsorber/LeanWaterRecycleFlow",
    "RecyclingAbsorber/TopPressure",
    "RecyclingAbsorber/TopOutRecycleGasTemperature",
    "RecyclingAbsorber/RecycleGasTemperature",
    "RecyclingAbsorber/MiddleTrayValve",
    "RecyclingAbsorber/BottomLevel",
    "RecyclingAbsorber/BottomOutTemperature",
    "RecyclingAbsorber/BottomOutFlow",
    "RecyclingAbsorber/BottomOutpH",
    "RecyclingStripper/MiddleTrayTemperature",
    "RecyclingStripper/ReboilerFluidFlow",
    "RecyclingStripper/Tray25Temperature",
  ]
```

Or you can simply edit the telegraf.conf file to write data to InfluxDB. Eclipse BaSyx fetches data from InfluxDB as described in article, so you can also edit the "Query" parameter in AASX file by opening it with AASX Package Explorer. 










