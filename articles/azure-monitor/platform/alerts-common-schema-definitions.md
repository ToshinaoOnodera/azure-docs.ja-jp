---
title: Webhooks、Logic Apps、Azure Functions、Automation Runbooks の共通アラート スキーマ定義
description: Webhooks、Logic Apps、Azure Functions、Automation Runbooks の共通アラート スキーマ定義について説明します
author: anantr
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 03/14/2019
ms.author: anantr
ms.component: alerts
ms.openlocfilehash: e29a1f5d1e258ab66540010dc12f9326b8fd57a2
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "60775748"
---
# <a name="common-alert-schema-definitions"></a>共通アラート スキーマ定義

この記事では、Webhooks、Logic Apps、Azure Functions、Automation Runbooks の[共通アラート スキーマ定義](https://aka.ms/commonAlertSchemaDocs)について説明します。 

## <a name="overview"></a>概要

すべてのアラート インスタンスでは、**影響を受けたリソース**および**アラートの原因**が記述されており、これらのインスタンスは次のセクションの共通スキーマで記述されています。
* **要点**: すべてのアラートの種類において共通の一連の**標準化されたフィールド**。これらのフィールドでは、アラート対象の**リソース**と、追加の共通アラート メタデータ (重大度や説明など) が記述されています。 
* **アラート コンテキスト**: **アラートの原因**が記述されているフィールドと、**アラートの種類に基づいて**異なるフィールドのセット。 たとえば、メトリック アラートの場合はメトリック名やメトリック値などのフィールドがアラート コンテキストにあり、アクティビティ ログ アラートの場合はそのアラートを生成したイベントに関する情報があります。 

##### <a name="sample-alert-payload"></a>アラートのペイロードのサンプル
```json
{
  "schemaId": "azureMonitorCommonAlertSchema",
  "data": {
    "essentials": {
      "alertId": "/subscriptions/<subscription ID>/providers/Microsoft.AlertsManagement/alerts/b9569717-bc32-442f-add5-83a997729330",
      "alertRule": "WCUS-R2-Gen2",
      "severity": "Sev3",
      "signalType": "Metric",
      "monitorCondition": "Resolved",
      "monitoringService": "Platform",
      "alertTargetIDs": [
        "/subscriptions/<subscription ID>/resourcegroups/pipelinealertrg/providers/microsoft.compute/virtualmachines/wcus-r2-gen2"
      ],
      "originAlertId": "3f2d4487-b0fc-4125-8bd5-7ad17384221e_PipeLineAlertRG_microsoft.insights_metricAlerts_WCUS-R2-Gen2_-117781227",
      "firedDateTime": "2019-03-22T13:58:24.3713213Z",
      "resolvedDateTime": "2019-03-22T14:03:16.2246313Z",
      "description": "",
      "essentialsVersion": "1.0",
      "alertContextVersion": "1.0"
    },
    "alertContext": {
      "properties": null,
      "conditionType": "SingleResourceMultipleMetricCriteria",
      "condition": {
        "windowSize": "PT5M",
        "allOf": [
          {
            "metricName": "Percentage CPU",
            "metricNamespace": "Microsoft.Compute/virtualMachines",
            "operator": "GreaterThan",
            "threshold": "25",
            "timeAggregation": "Average",
            "dimensions": [
              {
                "name": "ResourceId",
                "value": "3efad9dc-3d50-4eac-9c87-8b3fd6f97e4e"
              }
            ],
            "metricValue": 7.727
          }
        ]
      }
    }
  }
}
```

## <a name="essentials-fields"></a>"essentials" のフィールド

| フィールド | 説明|
|:---|:---|
| alertId | アラート インスタンスを一意に識別する GUID。 |
| alertRule | そのアラート インスタンスを生成したアラート ルールの名前。 |
| Severity | アラートの重大度。 指定できる値Sev0、Sev1、Sev2、Sev3、Sev4 |
| signalType | アラート ルールが定義されていたシグナルを示します。 指定できる値Metric、Log、Activity Log |
| monitorCondition | アラートが発生すると、アラートの監視条件は "Fired" に設定されます。 アラート発生の原因になった状態が解消されると、監視条件は "Resolved" に設定されます。   |
| monitoringService | アラートを生成した監視サービスまたはソリューション。 アラート コンテキストのフィールドは、監視サービスによって決まります。 |
| alertTargetIds | アラートの影響を受けたすべてのターゲットの ARM ID のリスト。 Log Analytics ワークスペースまたは Application Insights インスタンスで定義されているログ アラートの場合は、それぞれのワークスペース/アプリケーションになります。 |
| originAlertId | 生成元の監視サービスによって生成された警告インスタンスの ID。 |
| firedDateTime | 警告インスタンスが生成された日時 (UTC) |
| resolvedDateTime | アラート インスタンスの監視状態が "Resolved" に設定された日時 (UTC)。 現在はメトリック アラートに対してのみ適用されます。|
| description | アラート ルールで定義されている説明 |
|essentialsVersion| essentials セクションのバージョン番号。|
|alertContextVersion | alertContext セクションのバージョン番号 |

##### <a name="sample-values"></a>サンプルの値
```json
{
  "essentials": {
    "alertId": "/subscriptions/<subscription ID>/providers/Microsoft.AlertsManagement/alerts/b9569717-bc32-442f-add5-83a997729330",
    "alertRule": "Contoso IT Metric Alert",
    "severity": "Sev3",
    "signalType": "Metric",
    "monitorCondition": "Fired",
    "monitoringService": "Platform",
    "alertTargetIDs": [
      "/subscriptions/<subscription ID>/resourceGroups/aimon-rg/providers/Microsoft.Insights/components/ai-orion-int-fe"
    ],
    "originAlertId": "74ff8faa0c79db6084969cf7c72b0710e51aec70b4f332c719ab5307227a984f",
    "firedDateTime": "2019-03-26T05:25:50.4994863Z",
    "description": "Test Metric alert",
    "essentialsVersion": "1.0",
    "alertContextVersion": "1.0"
  }
}
```

## <a name="alert-context-fields"></a>"alertContext" のフィールド

### <a name="metric-alerts"></a>メトリック アラート

#### <a name="monitoringservice--platform"></a>monitoringService = "Platform"

##### <a name="sample-values"></a>サンプルの値
```json
{
  "alertContext": {
      "properties": null,
      "conditionType": "SingleResourceMultipleMetricCriteria",
      "condition": {
        "windowSize": "PT5M",
        "allOf": [
          {
            "metricName": "Percentage CPU",
            "metricNamespace": "Microsoft.Compute/virtualMachines",
            "operator": "GreaterThan",
            "threshold": "25",
            "timeAggregation": "Average",
            "dimensions": [
              {
                "name": "ResourceId",
                "value": "3efad9dc-3d50-4eac-9c87-8b3fd6f97e4e"
              }
            ],
            "metricValue": 31.1105
          }
        ],
        "windowStartTime": "2019-03-22T13:40:03.064Z",
        "windowEndTime": "2019-03-22T13:45:03.064Z"
      }
    }
}
```

### <a name="log-alerts"></a>ログ アラート

> [!NOTE]
> 既存のログ アラートにカスタム JSON オプションを使用した場合、カスタマイズ内容は共通スキーマに保存されません。

#### <a name="monitoringservice--log-analytics"></a>monitoringService = "Log Analytics"

##### <a name="sample-values"></a>サンプルの値
```json
{
  "alertContext": {
      "SearchQuery": "search * \n| where Type == \"Heartbeat\" \n| where Category == \"Direct Agent\" \n| where TimeGenerated > ago(30m) ",
      "SearchIntervalStartTimeUtc": "3/22/2019 1:36:31 PM",
      "SearchIntervalEndtimeUtc": "3/22/2019 1:51:31 PM",
      "ResultCount": 15,
      "LinkToSearchResults": "https://portal.azure.com#@72f988bf-86f1-41af-91ab-2d7cd011db47/blade/Microsoft_OperationsManagementSuite_Workspace/AnalyticsBlade/initiator/AnalyticsShareLinkToQuery/isQueryEditorVisible/true/scope/%7B%22resources%22%3A%5B%7B%22resourceId%22%3A%22%2Fsubscriptions%<subscription ID>%2FresourceGroups%2Fpipelinealertrg%2Fproviders%2FMicrosoft.OperationalInsights%2Fworkspaces%2FINC-OmsAlertRunner%22%7D%5D%7D/query/search%20%2A%20%0A%7C%20where%20Type%20%3D%3D%20%22Heartbeat%22%20%0A%7C%20where%20Category%20%3D%3D%20%22Direct%20Agent%22%20%0A%7C%20where%20TimeGenerated%20%3E%20%28datetime%282019-03-22T13%3A51%3A31.0000000%29%20-%2030m%29%20%20/isQuerybase64Compressed/false/timespanInIsoFormat/2019-03-22T13%3a36%3a31.0000000Z%2f2019-03-22T13%3a51%3a31.0000000Z",
      "SeverityDescription": "Warning",
      "WorkspaceId": "2a1f50a7-ef97-420c-9d14-938e77c2a929",
      "SearchIntervalDurationMin": "15",
      "AffectedConfigurationItems": [
        "INC-Gen2Alert"
      ],
      "SearchIntervalInMinutes": "15",
      "Threshold": 10000,
      "Operator": "Less Than"
    }
}
```

#### <a name="monitoringservice--application-insights"></a>monitoringService = "Application Insights"

##### <a name="sample-values"></a>サンプルの値
```json
{
  "alertContext": {
      "SearchQuery": "search *",
      "SearchIntervalStartTimeUtc": "3/22/2019 1:36:33 PM",
      "SearchIntervalEndtimeUtc": "3/22/2019 1:51:33 PM",
      "ResultCount": 0,
      "LinkToSearchResults": "https://portal.azure.com#@72f988bf-86f1-41af-91ab-2d7cd011db47/blade/Microsoft_OperationsManagementSuite_Workspace/AnalyticsBlade/initiator/AnalyticsShareLinkToQuery/isQueryEditorVisible/true/scope/%7B%22resources%22%3A%5B%7B%22resourceId%22%3A%22%2Fsubscriptions%<subscription ID>%2FresourceGroups%2FPipeLineAlertRG%2Fproviders%2Fmicrosoft.insights%2Fcomponents%2FWEU-AIRunner%22%7D%5D%7D/query/search%20%2A/isQuerybase64Compressed/false/timespanInIsoFormat/2019-03-22T13%3a36%3a33.0000000Z%2f2019-03-22T13%3a51%3a33.0000000Z",
      "SearchIntervalDurationMin": "15",
      "SearchIntervalInMinutes": "15",
      "Threshold": 10000,
      "Operator": "Less Than",
      "ApplicationId": "8e20151d-75b2-4d66-b965-153fb69d65a6"
    }
}
```

### <a name="activity-log-alerts"></a>アクティビティ ログ アラート

#### <a name="monitoringservice--activity-log---administrative"></a>monitoringService = "Activity Log - Administrative"

##### <a name="sample-values"></a>サンプルの値
```json
{
  "alertContext": {
      "authorization": {
        "action": "Microsoft.Compute/virtualMachines/restart/action",
        "scope": "/subscriptions/<subscription ID>/resourceGroups/PipeLineAlertRG/providers/Microsoft.Compute/virtualMachines/WCUS-R2-ActLog"
      },
      "channels": "Operation",
      "claims": "{\"aud\":\"https://management.core.windows.net/\",\"iss\":\"https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/\",\"iat\":\"1553260826\",\"nbf\":\"1553260826\",\"exp\":\"1553264726\",\"aio\":\"42JgYNjdt+rr+3j/dx68v018XhuFAwA=\",\"appid\":\"e9a02282-074f-45cf-93b0-50568e0e7e50\",\"appidacr\":\"2\",\"http://schemas.microsoft.com/identity/claims/identityprovider\":\"https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/\",\"http://schemas.microsoft.com/identity/claims/objectidentifier\":\"9778283b-b94c-4ac6-8a41-d5b493d03aa3\",\"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier\":\"9778283b-b94c-4ac6-8a41-d5b493d03aa3\",\"http://schemas.microsoft.com/identity/claims/tenantid\":\"72f988bf-86f1-41af-91ab-2d7cd011db47\",\"uti\":\"v5wYC9t9ekuA2rkZSVZbAA\",\"ver\":\"1.0\"}",
      "caller": "9778283b-b94c-4ac6-8a41-d5b493d03aa3",
      "correlationId": "8ee9c32a-92a1-4a8f-989c-b0ba09292a91",
      "eventSource": "Administrative",
      "eventTimestamp": "2019-03-22T13:56:31.2917159+00:00",
      "eventDataId": "161fda7e-1cb4-4bc5-9c90-857c55a8f57b",
      "level": "Informational",
      "operationName": "Microsoft.Compute/virtualMachines/restart/action",
      "operationId": "310db69b-690f-436b-b740-6103ab6b0cba",
      "status": "Succeeded",
      "subStatus": "",
      "submissionTimestamp": "2019-03-22T13:56:54.067593+00:00"
    }
}
```

## <a name="next-steps"></a>次の手順

- [共通アラート スキーマの詳細を確認する](https://aka.ms/commonAlertSchemaDocs)


