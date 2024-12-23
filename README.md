# AAS_Tools
This is the documentation of the referenced tools used in Asset Administration Shell Tool Comparison: A Case Study with Real Digital Twins Used in Petrochemical Industry.

**GitHub repositories of open source implementations can be found below:**

[FA³ST Service](https://github.com/FraunhoferIOSB/FAAAST-Service)

[Eclipse BaSyx™](https://github.com/eclipse-basyx)

[Eclipse AASX Server](https://github.com/eclipse-aaspe/server)

[NOVA Asset Administration Shell](https://gitlab.com/novaas/catalog/nova-school-of-science-and-technology/novaas)


Docker compose files can be achieved from the repositories.

Additionally, our AASX is created with [AASX Package Explorer (v2024-06-10.alpha)](https://github.com/eclipse-aaspe/package-explorer/releases/tag/v2024-06-10.alpha). File can be tested with 3 open sources which are Eclipse BaSyx™, Eclipse AASX Server and FA³ST Service.
AASX Package Explorer (v2024-06-10.alpha) supports only metamodel V3, so created AASX file is not compatible with NOVAAS. For testing NOVAAS, an example AASX file can be created with Metamodel V2 using [aasx-package-explorer.2022-05-10](https://github.com/admin-shell-io/aasx-package-explorer/releases/tag/v2022-05-10).

**Testing Eclipse BaSyx**

Eclipse BaSyx has import/export function for AASX or JSON files in the UI (localhost:3000 by default.) Once AASX file imported file will be displayed on dashboard. For other operations endpoints listed as default.
![image](https://github.com/user-attachments/assets/433870e3-42d6-432e-a62e-b8e27779c667)

**Testing AASX Server**

Download and export zip file in a folder. Then go to AasxServerBlazor>aasxs directory, add the Industrial_Column_Assets_Merged.aasx inside this folder and run startForDemo.bat or startForDemo.sh. GUI will be hosted on localhost:5001. 

**Testing FA³ST Service**

Download the jar file , then run this command in  CLI "java -jar starter-{version}.jar --model path_to_directory/Industrial_Column_Assets_Merged.aasx --no-validation" .





