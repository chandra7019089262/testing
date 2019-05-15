# Prodapt Automated VNF Certification Framework 

# Initial_Steps 
* All Prerequisites condition should be Implemented, Refer [Prerequisites](#prerequisites)
* Place all the configuration files such as onapconfig.json, osmconfig.json and etc., in the __ConfigFilesPath__ (VNFCertification\Trunk\etc\conf)
* Place all the data files such as SDNCPreload_vFW.json, OSM_VNFD_Cirros_m1_tiny.json and etc., in the __DataFilesPath__ (VNFCertification\Trunk\etc\data)
* External Expose IP should be changed to ONAP Portal IP in onapconfig.json file, present in location VNFCertification\Trunk\etc\conf
* Subscriber Name should be changed inside VNFCertification\Trunk\etc\conf\onapconfig.json file of following two json path.
  * $.serviceinstancecreate.data.requestDetails.subscriberInfo.globalSubscriberId
  * $.serviceInstanceDelete.uri (/aai/v14/business/customers/customer/**_<Subscriber_Name>_**/service-subscriptions/service-subscription/vFWCL/service-instances/service-instance)
* SDNCPreload_vFW.json of location VNFCertification\Trunk\etc\data need to be modified according to the reqirements.

 

# **Execution Steps** :
* Modify required changes in the TestData of location VNFCertification\Trunk\etc\data\TestData, Refer [Testdata_ONAP.json](#Testdata-ONAP) / [Testdata_OSM.json](#Testdata-OSM)
* Build TestPlan as per requirement, Refer [TestPlan.txt](#TestPlan)
* Run robot script 
    ```json
    Run test suites by providing following argument in the Ride UI.
    --argumentfile <Path_for_TestPlan>
    Ex: --argumentfile C:\\Users\\prodapt\\Desktop\\Prodapt\\01a_Test_Plan_HealthCheck_ONAP.txt
                       (OR)
    Run test suites by following command in CLI
    robot --argumentfile <Path_for_TestPlan> <TestSuite>
    Ex:  robot --argumentfile C:\\Users\\prodapt\\Desktop\\Prodapt\\01a_Test_Plan_HealthCheck_ONAP.txt
    ```
* Check the log and report generated for the test results




# Changes if Environment changed
* External Expose IP should be changed to ONAP Portal IP in onapconfig.json file, present in location VNFCertification\Trunk\etc\conf
* Subscriber Name should be changed inside onapconfig.json file of following two locations.
  * $.serviceinstancecreate.data.requestDetails.subscriberInfo.globalSubscriberId
  * $.serviceInstanceDelete.uri (/aai/v14/business/customers/customer/**_<Subscriber_Name>_**/service-subscriptions/service-subscription/vFWCL/service-instances/service-instance) (Change <Subscriber_Name> in the uri)
* SDNCPreload_vFW.json of location VNFCertification\Trunk\etc\data need to be modified according to the reqirements.
* Run [Execution Steps](Execution-Steps)




# Prerequisites
- Place the _vnfcertification_  folder(which is present in the following path VNFCertification\src\main) in site-packages path of your python library. Eg: C:\Python27\Lib\site-packages
- All python libraries required for the test case should be installed

    ```sh
    requirement.txt file contains libraries that needs to be installed for current platform.
    These can be installed using below command.
    Ex: pip install -r requirement.txt
    ```
- Replace the htmldata folder in site-packages/robot/ path of your python library (Eg: C:\Python27\Lib\site-packages\robot\) with _htmldata_ folder (which is present in the following path VNFCertification\Trunk\src\main\resources\report).




# Testdata ONAP

    ### Details of Testdata_ONAP.json
    * **_configFilePath_** : Path of the Configuration files
    * **_dataFilePath_** : Path of the Data files
    * **_instancesDataFilePath_** : Path where instance details are to be saved
    * **_csarFileName_** : Name of the CSAR file
    * **_vspName_** : Name of the Software Product
    * **_serviceInstanceName_** : Name of the Service Instance
    * **_vnfInstanceName_** : Name of the VNF Instance
    * **_vfmodulename_** : Name of the VFModule
    * **_vFWImageName_** : Image used to spawn up the vFW Instance
    * **_vFWFlavorName_** : Name of the Flavor for Instance 
    * **_defaultPlaybookPolicy_** : Playbook policy initialy used for an Instance
    * **_playbookPolicy_** : Playbook name used to update the firewall config (default value should be defaultowrt or defaultpfsense)
    * **_clientIP_** : Public IP address of the client
    * **_firewallIP_** : Public IP address of the firewall
    * **_serverIP_** : Private IP address of the server
    * **_clientUserName_** : UserName for client instance login
    * **_clientPassword_** : Password for client instance login

    ### Example
    ```json
    {
    "configFilePath": "C:\\Users\\Prodapt\\Desktop\\VNFCertification\\Trunk\\etc\\conf",
    "dataFilePath": "C:\\Users\\Prodapt\\Desktop\\VNFCertification\\Trunk\\etc\\data",
    "instancesDataFilePath": "C:\\Users\\Prodapt\\Desktop\\VNFCertification\\Trunk\\etc\\data\\TestData\\InstancesData_ONAP.json",
    "csarFileName": "prodapt_csar_v4.zip",
    "vspName": "prodapt_vsp_test101",
    "serviceInstanceName":  "prodapt-vfw-service-1000-SI-2",
    "vnfInstanceName":  "prodapt-vfw-service-1000-VNF-2",
    "vfmodulename": "prodapt-vfw-service-1000-VF-2",
    "vFWImageName": "vFWRT",
    "vFWFlavorName": "m1.medium",
    "defaultPlaybookPolicy": "defaultowrt",
    "playbookPolicy": "owrt_policy@3.01.yml",
    "clientIP": "10.168.155.151",
    "firewallIP": "10.168.155.150",
    "serverIP": "10.5.0.151",
    "clientUserName": "cadmin",
    "clientPassword": "cadmin123"
    }
    ```




# Testdata OSM
    ### Details of Testdata_OSM.josn
    * **_nsId_** : ID of Network Service Created
    * **_osmVnfdFileName_** : Name of OSM VNF Descriptor file
    * **_configFilePath_** : Path of the Configuration files
    * **_nsdId_** : ID of Network Service Descriptor Onboarded
    * **_vnfdId_** : ID of VNF Descriptor Onboarded
    * **_nsName_** : Name of the Network Service to be created
    * **_osmBaseURL_** : Base URL of the OSM
    * **_dataFilePath_** : Path of the Data files
    * **_osmPortNumber_** : Port Number of the OSM
    * **_vimAccountId_** : ID of the VIM Account linked with Openstack
    * **_osmNsdFileName_** : Name of the OSM NS Descriptor file

    ### Example
    ```json
    {
	"nsId": "dummyId",
	"osmVnfdFileName": "OSM_VNFD_OpenWRT_m1_small.json",
	"configFilePath": "C:\\Users\\Prodapt\\Desktop\\VNFCertification\\Trunk\\etc\\conf",
	"nsdId": "dummyId",
	"vnfdId": "dummyId",
	"nsName": "prodapt_robo2_ns",
	"osmBaseURL": "https://10.168.154.68",
	"dataFilePath": "C:\\Users\\Prodapt\\Desktop\\VNFCertification\\Trunk\\etc\\data",
	"osmPortNumber": "9999",
	"vimAccountId": "2515b6e3-3773-4e48-afc1-5e0ab56eec09",
	"osmNsdFileName": "OSM_NSD_OpenWRT_m1_small.json"
    }
    ```




# InstanceData ONAP
  ### Details of InstanceData_ONAP.json
  * **_vnfInstanceId_** : ID of the VNF Instance
  * **_distributedServiceUUID_** : UUID of the distributed Service Model
  * **_serviceInstanceId_** : Id of the Service Instance created
  * **_vfModuleId_** : VF module Instance ID
  ### Example
  ```
  {
  "vnfInstanceId": "fb959252-c686-4545-b873-3abfe23f6f62", 
  "distributedServiceUUID": "1a4e23f9-3376-4521-9afd-32eb06932445", 
  "serviceInstanceId": "605d0c38-5307-48eb-b575-c061e97bf9e8", 
  "vfModuleId": "346f814c-9edf-4406-8d37-b32876640ac2"
  }
  ```
- Related File is present for OSM. Refer InstanceData_OSM.json file for information.





# TestPlan
  ### Details of TestPlan
  * **_-v Orchestrator:<Orchestrator_name>_**    : Name of Orchestrator using for testing.
  * **_-v Test_Data_File_Path:<Path_of_TestData>_**    : Path of the TestData 
  * **_-v username:<User_name>_**    : Username of the component (Used for login and version check)
  * **_-v password:<password>_**    : Password of the component (Used for login and version check)

  * **_-t <TestCase>_**    : Specify TestCases need to be Executed.
### Example
  ```
    -v Orchestrator:onap
    -v Test_Data_File_Path:C:\\Users\\prodapt\\Desktop\\VNFCertification\\Trunk\\etc\\data\\TestData\\TestData_ONAP1.json
    -v username:aai@aai.onap.org
    -v password:demo123456!

    -t Login Check
    -t Version Check
  ```
