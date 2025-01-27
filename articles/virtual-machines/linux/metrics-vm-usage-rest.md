---
title: REST API を使用して Azure 仮想マシンの使用状況データを取得する | Microsoft Docs
description: Azure REST API を使用して、仮想マシンの使用率メトリックを収集します。
services: virtual-machines
author: rloutlaw
ms.reviewer: routlaw
manager: jeconnoc
ms.service: load-balancer
ms.custom: REST
ms.topic: article
ms.date: 06/13/2018
ms.author: routlaw
ms.openlocfilehash: 924154a64673b4ff646f3b6ece373b278ee37181
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "60773266"
---
# <a name="get-virtual-machine-usage-metrics-using-the-rest-api"></a>REST API を使用して仮想マシンの使用状況のメトリックを取得する

この例では、[Azure REST API](/rest/api/azure/) を使用して、[Linux 仮想マシン](https://docs.microsoft.com/azure/virtual-machines/linux/monitor)の CPU 使用率を取得する方法を示します。

完全なリファレンス ドキュメントと REST API の他の例は、[Azure Monitor REST リファレンス](/rest/api/monitor)で確認できます。 

## <a name="build-the-request"></a>要求を作成する

仮想マシンから [CPU の割合メトリック](/azure/monitoring-and-diagnostics/monitoring-supported-metrics#microsoftcomputevirtualmachines)を収集するには、次の GET 要求を使用します。

```http
GET https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmname}/providers/microsoft.insights/metrics?api-version=2018-01-01&metricnames=Percentage%20CPU&timespan=2018-06-05T03:00:00Z/2018-06-07T03:00:00Z
```

### <a name="request-headers"></a>要求ヘッダー

次のヘッダーは必須です｡ 

|要求ヘッダー|説明|  
|--------------------|-----------------|  
|*Content-Type:*|必須。 `application/json` を設定します。|  
|*Authorization:*|必須。 有効な `Bearer` [ アクセス トークン](/rest/api/azure/#authorization-code-grant-interactive-clients)を設定します｡ |  

### <a name="uri-parameters"></a>URI パラメーター

| Name | 説明 |
| :--- | :---------- |
| subscriptionId | Azure サブスクリプションを識別するサブスクリプション ID。 複数のサブスクリプションをお持ちの場合は､[Working with multiple subscriptions](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli?view=azure-cli-latest)を参照してください｡ |
| resourceGroupName | リソースに関連付けられている Azure リソース グループの名前。 この値は、Azure Resource Manager API、CLI、またはポータルから取得できます。 |
| vmname | Azure 仮想マシンの名前。 |
| metricnames | 有効な[Load Balancer メトリック](/azure/load-balancer/load-balancer-standard-diagnostics)のコンマ区切りリスト。 |
| api-version | 要求で使用する API のバージョン。<br /><br /> このドキュメントでは、api-version `2018-01-01` を使用し、上記の URL に含まれています。  |
| TimeSpan | 返されるメトリックの時間範囲を定義する次の形式の文字列: `startDateTime_ISO/endDateTime_ISO`。 この省略可能なパラメーターは、例では 1 日分のデータを返すように設定されています。 |
| &nbsp; | &nbsp; |

### <a name="request-body"></a>要求本文

この操作では、要求本文は必要ありません。

## <a name="handle-the-response"></a>応答の処理

メトリック値の一覧が正常に返された場合は、状態コード 200 が返されます。 エラー コードの完全な一覧は、[リファレンス ドキュメント](/rest/api/monitor/metrics/list#errorresponse)で確認できます。

## <a name="example-response"></a>応答の例 

```json
{
    "cost": 0,
    "timespan": "2018-06-08T23:48:10Z/2018-06-09T00:48:10Z",
    "interval": "PT1M",
    "value": [
        {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmname}/providers/microsoft.insights/metrics?api-version=2018-01-01&metricnames=Percentage%20CPU",
            "type": "Microsoft.Insights/metrics",
            "name": {
                "value": "Percentage CPU",
                "localizedValue": "Percentage CPU"
            },
            "unit": "Percent",
            "timeseries": [
                {
                    "metadatavalues": [],
                    "data": [
                        {
                            "timeStamp": "2018-06-08T23:48:00Z",
                            "average": 0.44
                        },
                        {
                            "timeStamp": "2018-06-08T23:49:00Z",
                            "average": 0.31
                        },
                        {
                            "timeStamp": "2018-06-08T23:50:00Z",
                            "average": 0.29
                        },
                        {
                            "timeStamp": "2018-06-08T23:51:00Z",
                            "average": 0.29
                        },
                        {
                            "timeStamp": "2018-06-08T23:52:00Z",
                            "average": 0.285
                        } ]
                } ]
        } ]
}
```
