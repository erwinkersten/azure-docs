---
title: Supported resources for metric alerts in Azure Monitor
description: Reference on support metrics and logs for metric alerts in Azure Monitor
author: harelbr
ms.author: harelbr
services: monitoring
ms.topic: conceptual
ms.date: 9/14/2022
ms.reviwer: harelbr
---

# Supported resources for metric alerts in Azure Monitor

Azure Monitor now supports a [new metric alert type](./alerts-overview.md), which has significant benefits over the older [classic metric alerts](./alerts-classic.overview.md). Metrics are available for a [large list of Azure services](../essentials/metrics-supported.md). The newer alerts support a growing subset of the resource types. This article lists that subset.

You can also use newer metric alerts on popular log data stored in a Log Analytics workspace extracted as metrics. For more information, see [Metric Alerts for Logs](./alerts-metric-logs.md).

## Portal, PowerShell, CLI, and REST support

Currently, you can create newer metric alerts only in the Azure portal, the [REST API](/rest/api/monitor/metricalerts/), or [Azure Resource Manager templates](./alerts-metric-create-templates.md). Support for configuring newer alerts by using PowerShell and the Azure CLI versions 2.0 and higher is coming soon.

## Metrics and dimensions supported

Newer metric alerts support alerting for metrics that use dimensions. You can use dimensions to filter your metric to the proper level. All supported metrics along with applicable dimensions can be explored and visualized from [Azure Monitor - Metrics explorer](../essentials/metrics-charts.md).

Here's the full list of Azure Monitor metric sources supported by the newer alerts:

|Resource type  |Dimensions supported |Multi-resource alerts| Metrics available|
|---------|---------|-----|----------|
|Microsoft.Aadiam/azureADMetrics | Yes | No | Azure Active Directory (metrics in private preview) |
|Microsoft.ApiManagement/service | Yes | No | [Azure API Management](../essentials/metrics-supported.md#microsoftapimanagementservice) |
|Microsoft.App/containerApps | Yes | No | Azure Container Apps |
|Microsoft.AppConfiguration/configurationStores |Yes | No | [Azure App Configuration](../essentials/metrics-supported.md#microsoftappconfigurationconfigurationstores) |
|Microsoft.AppPlatform/spring | Yes | No | [Azure Spring Cloud](../essentials/metrics-supported.md#microsoftappplatformspring) |
|Microsoft.Automation/automationAccounts | Yes| No | [Azure Automation accounts](../essentials/metrics-supported.md#microsoftautomationautomationaccounts) |
|Microsoft.AVS/privateClouds | No | No | [Azure VMware Solution](../essentials/metrics-supported.md) |
|Microsoft.Batch/batchAccounts | Yes | No | [Azure Batch accounts](../essentials/metrics-supported.md#microsoftbatchbatchaccounts) |
|Microsoft.Bing/accounts | Yes | No | [Bing accounts](../essentials/metrics-supported.md#microsoftmapsaccounts) |
|Microsoft.BotService/botServices | Yes | No | [Azure Bot Service](../essentials/metrics-supported.md#microsoftbotservicebotservices) |
|Microsoft.Cache/redis | Yes | Yes | [Azure Cache for Redis](../essentials/metrics-supported.md#microsoftcacheredis) |
|Microsoft.Cache/redisEnterprise | Yes | No | [Azure Cache for Redis Enterprise](../essentials/metrics-supported.md#microsoftcacheredisenterprise) |
|microsoft.Cdn/profiles | Yes | No | [Azure Content Delivery Network profiles](../essentials/metrics-supported.md#microsoftcdnprofiles) |
|Microsoft.ClassicCompute/domainNames/slots/roles | No | No | [Azure Cloud Services (classic)](../essentials/metrics-supported.md#microsoftclassiccomputedomainnamesslotsroles) |
|Microsoft.ClassicCompute/virtualMachines | No | No | [Azure Virtual Machines (classic)](../essentials/metrics-supported.md#microsoftclassiccomputevirtualmachines) |
|Microsoft.ClassicStorage/storageAccounts | Yes | No | [Azure Storage accounts (classic)](../essentials/metrics-supported.md#microsoftclassicstoragestorageaccounts) |
|Microsoft.ClassicStorage/storageAccounts/blobServices | Yes | No | [Azure Blob Storage accounts (classic)](../essentials/metrics-supported.md#microsoftclassicstoragestorageaccountsblobservices) |
|Microsoft.ClassicStorage/storageAccounts/fileServices | Yes | No | [Azure Files storage accounts (classic)](../essentials/metrics-supported.md#microsoftclassicstoragestorageaccountsfileservices) |
|Microsoft.ClassicStorage/storageAccounts/queueServices | Yes | No | [Azure Queue Storage accounts (classic)](../essentials/metrics-supported.md#microsoftclassicstoragestorageaccountsqueueservices) |
|Microsoft.ClassicStorage/storageAccounts/tableServices | Yes | No | [Azure Table Storage accounts (classic)](../essentials/metrics-supported.md#microsoftclassicstoragestorageaccountstableservices) |
|Microsoft.CognitiveServices/accounts | Yes | No | [Azure Cognitive Services](../essentials/metrics-supported.md#microsoftcognitiveservicesaccounts) |
|Microsoft.Compute/cloudServices | Yes | No |  [Azure Cloud Services](../essentials/metrics-supported.md#microsoftcomputecloudservices) |
|Microsoft.Compute/cloudServices/roles | Yes | No |  [Azure Cloud Services roles](../essentials/metrics-supported.md#microsoftcomputecloudservicesroles) |
|Microsoft.Compute/virtualMachines | Yes | Yes<sup>1</sup> | [Azure Virtual Machines](../essentials/metrics-supported.md#microsoftcomputevirtualmachines) |
|Microsoft.Compute/virtualMachineScaleSets | Yes | No |[Azure Virtual Machine Scale Sets](../essentials/metrics-supported.md#microsoftcomputevirtualmachinescalesets) |
|Microsoft.ConnectedVehicle/platformAccounts | Yes | No |[Connected Vehicle Platform Accounts](../essentials/metrics-supported.md) |
|Microsoft.ContainerInstance/containerGroups | Yes| No | [Container groups](../essentials/metrics-supported.md#microsoftcontainerinstancecontainergroups) |
|Microsoft.ContainerRegistry/registries | No | No | [Azure Container Registry](../essentials/metrics-supported.md#microsoftcontainerregistryregistries) |
|Microsoft.ContainerService/managedClusters | Yes | No | [Managed clusters](../essentials/metrics-supported.md#microsoftcontainerservicemanagedclusters) |
|Microsoft.DataBoxEdge/dataBoxEdgeDevices | Yes | Yes | [Azure Data Box](../essentials/metrics-supported.md#microsoftdataboxedgedataboxedgedevices) |
|Microsoft.DataFactory/datafactories| Yes| No | [Azure Data Factory V1](../essentials/metrics-supported.md#microsoftdatafactorydatafactories) |
|Microsoft.DataFactory/factories |Yes | No | [Azure Data Factory V2](../essentials/metrics-supported.md#microsoftdatafactoryfactories) |
|Microsoft.DataProtection/backupVaults | Yes | Yes | Azure Backup vaults |
|Microsoft.DataShare/accounts | Yes | No | [Azure Data Share](../essentials/metrics-supported.md#microsoftdatashareaccounts) |
|Microsoft.DBforMariaDB/servers | No | No | [Azure Database for MariaDB](../essentials/metrics-supported.md#microsoftdbformariadbservers) |
|Microsoft.DBforMySQL/servers | No | No |[Azure Database for MySQL](../essentials/metrics-supported.md#microsoftdbformysqlservers)|
|Microsoft.DBforPostgreSQL/flexibleServers | Yes | Yes | [Azure Database for PostgreSQL (flexible servers)](../essentials/metrics-supported.md#microsoftdbforpostgresqlflexibleservers)|
|Microsoft.DBforPostgreSQL/serverGroupsv2 | Yes | No | Azure Database for PostgreSQL (hyperscale) |
|Microsoft.DBforPostgreSQL/servers | No | No | [Azure Database for PostgreSQL](../essentials/metrics-supported.md#microsoftdbforpostgresqlservers)|
|Microsoft.DBforPostgreSQL/serversv2 | No | No | [Azure Database for PostgreSQL V2](../essentials/metrics-supported.md#microsoftdbforpostgresqlserversv2)|
|Microsoft.Devices/IotHubs | Yes | No |[Azure IoT Hub](../essentials/metrics-supported.md#microsoftdevicesiothubs) |
|Microsoft.Devices/provisioningServices| Yes | No | [Device Provisioning Service](../essentials/metrics-supported.md#microsoftdevicesprovisioningservices) |
|Microsoft.DigitalTwins/digitalTwinsInstances | Yes | No | [Azure Digital Twins](../essentials/metrics-supported.md#microsoftdigitaltwinsdigitaltwinsinstances) |
|Microsoft.DocumentDB/databaseAccounts | Yes | No | [Azure Cosmos DB](../essentials/metrics-supported.md#microsoftdocumentdbdatabaseaccounts) |
|Microsoft.EventGrid/domains | Yes | No | [Azure Event Grid domains](../essentials/metrics-supported.md#microsofteventgriddomains) |
|Microsoft.EventGrid/systemTopics | Yes | No | [Azure Event Grid system topics](../essentials/metrics-supported.md#microsofteventgridsystemtopics) |
|Microsoft.EventGrid/topics |Yes | No | [Azure Event Grid topics](../essentials/metrics-supported.md#microsofteventgridtopics) |
|Microsoft.EventHub/clusters |Yes| No | [Azure Event Hubs clusters](../essentials/metrics-supported.md#microsofteventhubclusters) |
|Microsoft.EventHub/namespaces |Yes| No | [Azure Event Hubs](../essentials/metrics-supported.md#microsofteventhubnamespaces) |
|Microsoft.HDInsight/clusters | Yes | No | [Azure HDInsight clusters](../essentials/metrics-supported.md#microsofthdinsightclusters) |
|Microsoft.Insights/Components | Yes | No | [Application Insights](../essentials/metrics-supported.md#microsoftinsightscomponents) |
|Microsoft.KeyVault/vaults | Yes |Yes |[Azure Key Vault](../essentials/metrics-supported.md#microsoftkeyvaultvaults)|
|Microsoft.Kusto/Clusters | Yes |No |[Data explorer clusters](../essentials/metrics-supported.md#microsoftkustoclusters)|
|Microsoft.Logic/integrationServiceEnvironments | Yes | No |[Azure Integration Services environments](../essentials/metrics-supported.md#microsoftlogicintegrationserviceenvironments) |
|Microsoft.Logic/workflows | No | No |[Azure Logic Apps](../essentials/metrics-supported.md#microsoftlogicworkflows) |
|Microsoft.MachineLearningServices/workspaces | Yes | No | [Azure Machine Learning](../essentials/metrics-supported.md#microsoftmachinelearningservicesworkspaces) |
|Microsoft.MachineLearningServices/workspaces/onlineEndpoints | Yes | No | Azure Machine Learning endpoints |
|Microsoft.MachineLearningServices/workspaces/onlineEndpoints/deployments | Yes | No | Azure Machine Learning endpoint deployments |
|Microsoft.Maps/accounts | Yes | No | [Azure Maps accounts](../essentials/metrics-supported.md#microsoftmapsaccounts) |
|Microsoft.Media/mediaservices | No | No | [Azure Media Services](../essentials/metrics-supported.md#microsoftmediamediaservices) |
|Microsoft.Media/mediaservices/streamingEndpoints | Yes | No | [Azure Media Services streaming endpoints](../essentials/metrics-supported.md#microsoftmediamediaservicesstreamingendpoints) |
|Microsoft.NetApp/netAppAccounts/capacityPools | Yes | Yes | [Azure NetApp Files capacity pools](../essentials/metrics-supported.md#microsoftnetappnetappaccountscapacitypools) |
|Microsoft.NetApp/netAppAccounts/capacityPools/volumes | Yes | Yes | [Azure NetApp Files volumes](../essentials/metrics-supported.md#microsoftnetappnetappaccountscapacitypoolsvolumes) |
|Microsoft.Network/applicationGateways | Yes | No | [Azure Application Gateway](../essentials/metrics-supported.md#microsoftnetworkapplicationgateways) |
|Microsoft.Network/azurefirewalls | Yes | No | [Azure Firewall](../essentials/metrics-supported.md#microsoftnetworkazurefirewalls) |
|Microsoft.Network/dnsZones | No | No | [Azure DNS zones](../essentials/metrics-supported.md#microsoftnetworkdnszones) |
|Microsoft.Network/expressRouteCircuits | Yes | No |[Azure ExpressRoute circuits](../essentials/metrics-supported.md#microsoftnetworkexpressroutecircuits) |
|Microsoft.Network/expressRouteGateways | Yes | No |[Azure ExpressRoute gateways](../essentials/metrics-supported.md#microsoftnetworkexpressroutegateways) |
|Microsoft.Network/expressRoutePorts | Yes | No |[Azure ExpressRoute direct](../essentials/metrics-supported.md#microsoftnetworkexpressrouteports) |
|Microsoft.Network/loadBalancers (only for Standard SKUs)| Yes| No | [Azure Load Balancer](../essentials/metrics-supported.md#microsoftnetworkloadbalancers) |
|Microsoft.Network/natGateways| No | No | [NAT Gateway](../essentials/metrics-supported.md#microsoftnetworknatgateways) |
|Microsoft.Network/privateEndpoints| No | No | [Private endpoints](../essentials/metrics-supported.md#microsoftnetworkprivateendpoints) |
|Microsoft.Network/privateLinkServices| No | No | [Azure Private Link services](../essentials/metrics-supported.md#microsoftnetworkprivatelinkservices) |
|Microsoft.Network/publicipaddresses | No | No | [Public IP addresses](../essentials/metrics-supported.md#microsoftnetworkpublicipaddresses)|
|Microsoft.Network/trafficManagerProfiles | Yes | No | [Azure Traffic Manager profiles](../essentials/metrics-supported.md#microsoftnetworktrafficmanagerprofiles) |
|Microsoft.OperationalInsights/workspaces| Yes | No | [Log Analytics workspaces](../essentials/metrics-supported.md#microsoftoperationalinsightsworkspaces)|
|Microsoft.Peering/peerings | Yes | No | [Azure Peering Service](../essentials/metrics-supported.md#microsoftpeeringpeerings) |
|Microsoft.Peering/peeringServices | Yes | No | [Azure Peering Service](../essentials/metrics-supported.md#microsoftpeeringpeeringservices) |
|Microsoft.PowerBIDedicated/capacities | No | No | [Power BI dedicated capacities](../essentials/metrics-supported.md#microsoftpowerbidedicatedcapacities) |
|Microsoft.Purview/accounts | Yes | No | [Azure Purview accounts](../essentials/metrics-supported.md#microsoftpurviewaccounts) |
|Microsoft.RecoveryServices/vaults | Yes | Yes | [Recovery Services vaults](../essentials/metrics-supported.md) |
|Microsoft.Relay/namespaces | Yes | No | [Relays](../essentials/metrics-supported.md#microsoftrelaynamespaces) |
|Microsoft.Search/searchServices | No | No | [Search services](../essentials/metrics-supported.md#microsoftsearchsearchservices) |
|Microsoft.ServiceBus/namespaces | Yes | No | [Azure Service Bus](../essentials/metrics-supported.md#microsoftservicebusnamespaces) |
|Microsoft.SignalRService/WebPubSub | Yes | No | [Azure Web PubSub service](../essentials/metrics-supported.md#microsoftsignalrservicewebpubsub) |
|Microsoft.Sql/managedInstances | No | No | [Azure SQL Managed Instance](../essentials/metrics-supported.md#microsoftsqlmanagedinstances) |
|Microsoft.Sql/servers/databases | No | Yes | [Azure SQL Database](../essentials/metrics-supported.md#microsoftsqlserversdatabases) |
|Microsoft.Sql/servers/elasticPools | No | Yes | [Azure SQL Database elastic pools](../essentials/metrics-supported.md#microsoftsqlserverselasticpools) |
|Microsoft.Storage/storageAccounts |Yes | No | [Azure Storage accounts](../essentials/metrics-supported.md#microsoftstoragestorageaccounts)|
|Microsoft.Storage/storageAccounts/blobServices | Yes| No | [Azure Blob Storage accounts](../essentials/metrics-supported.md#microsoftstoragestorageaccountsblobservices) |
|Microsoft.Storage/storageAccounts/fileServices | Yes| No | [Azure Files storage accounts](../essentials/metrics-supported.md#microsoftstoragestorageaccountsfileservices) |
|Microsoft.Storage/storageAccounts/queueServices | Yes| No | [Azure Queue Storage accounts](../essentials/metrics-supported.md#microsoftstoragestorageaccountsqueueservices) |
|Microsoft.Storage/storageAccounts/tableServices | Yes| No | [Azure Table Storage accounts](../essentials/metrics-supported.md#microsoftstoragestorageaccountstableservices) |
|Microsoft.StorageCache/caches | Yes | No | [Azure HPC Cache](../essentials/metrics-supported.md#microsoftstoragecachecaches) |
|Microsoft.StorageSync/storageSyncServices | Yes | No | [Storage sync services](../essentials/metrics-supported.md#microsoftstoragesyncstoragesyncservices) |
|Microsoft.StreamAnalytics/streamingjobs | Yes | No | [Azure Stream Analytics](../essentials/metrics-supported.md#microsoftstreamanalyticsstreamingjobs) |
|Microsoft.Synapse/workspaces | Yes | No | [Azure Synapse Analytics](../essentials/metrics-supported.md#microsoftsynapseworkspaces) |
|Microsoft.Synapse/workspaces/bigDataPools | Yes | No | [Azure Synapse Analytics Apache Spark pools](../essentials/metrics-supported.md#microsoftsynapseworkspacesbigdatapools) |
|Microsoft.Synapse/workspaces/sqlPools | Yes | No | [Azure Synapse Analytics SQL pools](../essentials/metrics-supported.md#microsoftsynapseworkspacessqlpools) |
|Microsoft.VMWareCloudSimple/virtualMachines | Yes | No | [CloudSimple virtual machines](../essentials/metrics-supported.md) |
|Microsoft.Web/containerApps | Yes | No | Azure Container Apps |
|Microsoft.Web/hostingEnvironments/multiRolePools | Yes | No | [Azure App Service environment multi-role pools](../essentials/metrics-supported.md#microsoftwebhostingenvironmentsmultirolepools)|
|Microsoft.Web/hostingEnvironments/workerPools | Yes | No | [Azure App Service environment worker pools](../essentials/metrics-supported.md#microsoftwebhostingenvironmentsworkerpools)|
|Microsoft.Web/serverfarms | Yes | No | [Azure App Service plans](../essentials/metrics-supported.md#microsoftwebserverfarms)|
|Microsoft.Web/sites | Yes | No | [Azure App Service and Azure Functions](../essentials/metrics-supported.md#microsoftwebsites)|
|Microsoft.Web/sites/slots | Yes | No | [Azure App Service slots](../essentials/metrics-supported.md#microsoftwebsitesslots)|

<sup>1</sup> Not supported for virtual machine network metrics such as Network In Total, Network Out Total, Inbound Flows, Outbound Flows, Inbound Flows Maximum Creation Rate, and Outbound Flows Maximum Creation Rate. Also not supported for custom metrics.

## Payload schema

> [!NOTE]
> You can also use the [common alert schema](./alerts-common-schema.md), which provides the advantage of having a single extensible and unified alert payload across all the alert services in Azure Monitor, for your webhook integrations. [Learn about the common alert schema definitions](./alerts-common-schema-definitions.md).​

The POST operation contains the following JSON payload and schema for all near newer metric alerts when an appropriately configured [action group](./action-groups.md) is used:

```json
{
  "schemaId": "AzureMonitorMetricAlert",
  "data": {
    "version": "2.0",
    "status": "Activated",
    "context": {
      "timestamp": "2018-02-28T10:44:10.1714014Z",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/microsoft.insights/metricAlerts/StorageCheck",
      "name": "StorageCheck",
      "description": "",
      "conditionType": "SingleResourceMultipleMetricCriteria",
      "severity":"3",
      "condition": {
        "windowSize": "PT5M",
        "allOf": [
          {
            "metricName": "Transactions",
            "metricNamespace":"microsoft.storage/storageAccounts",
            "dimensions": [
              {
                "name": "AccountResourceId",
                "value": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500"
              },
              {
                "name": "GeoType",
                "value": "Primary"
              }
            ],
            "operator": "GreaterThan",
            "threshold": "0",
            "timeAggregation": "PT5M",
            "metricValue": 1
          }
        ]
      },
      "subscriptionId": "00000000-0000-0000-0000-000000000000",
      "resourceGroupName": "Contoso",
      "resourceName": "diag500",
      "resourceType": "Microsoft.Storage/storageAccounts",
      "resourceId": "/subscriptions/1e3ff1c0-771a-4119-a03b-be82a51e232d/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500",
      "portalLink": "https://portal.azure.com/#resource//subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500"
    },
    "properties": {
      "key1": "value1",
      "key2": "value2"
    }
  }
}
```

## Next steps

* Learn more about the new [alerts experience](./alerts-overview.md).
* Learn about [log alerts in Azure](./alerts-unified-log.md).
* Learn about [alerts in Azure](./alerts-overview.md).
