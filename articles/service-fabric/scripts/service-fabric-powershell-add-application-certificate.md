---
title: Azure PowerShell のサンプル スクリプト - アプリケーション証明書のクラスターへの追加 | Microsoft Docs
description: Azure PowerShell のサンプル スクリプト - アプリケーション証明書の Service Fabric クラスターへの追加。
services: service-fabric
documentationcenter: ''
author: aljo-microsoft
manager: chackdan
editor: ''
tags: azure-service-management
ms.assetid: ''
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: sample
ms.date: 01/18/2018
ms.author: aljo
ms.custom: mvc
ms.openlocfilehash: 313a1b7e4f0109a0a5cb94214918d97c25b5cf5d
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "66153843"
---
# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a>アプリケーション証明書の Service Fabric クラスターへの追加

このサンプル スクリプトは、指定された Azure Key Vault 内に自己署名証明書を作成し、Service Fabric クラスターのすべてのノードにこの証明書をインストールします。 証明書はローカル フォルダーにもダウンロードされます。 ダウンロードされる証明書の名前は、キー コンテナー内の証明書の名前と同じです。 必要に応じてパラメーターをカスタマイズします。

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

必要に応じて、[Azure PowerShell ガイド](/powershell/azure/overview)の手順に従って Azure PowerShell をインストールし、`Connect-AzAccount` を実行して、Azure との接続を作成します。 

## <a name="sample-script"></a>サンプル スクリプト

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate to a cluster")]

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは以下のコマンドを使用します。表内の各コマンドは、それぞれのドキュメントにリンクされています。

| command | メモ |
|---|---|
| [Add-AzServiceFabricApplicationCertificate](/powershell/module/az.servicefabric/Add-azServiceFabricApplicationCertificate) | クラスターを構成する仮想マシン スケール セットに新しいアプリケーション証明書を追加します。  |

## <a name="next-steps"></a>次の手順

Azure PowerShell モジュールの詳細については、[Azure PowerShell のドキュメント](/powershell/azure/overview)を参照してください。

その他の Azure Service Fabric 用 Azure PowerShell サンプルは、[Azure PowerShell サンプル](../service-fabric-powershell-samples.md)のページにあります。
