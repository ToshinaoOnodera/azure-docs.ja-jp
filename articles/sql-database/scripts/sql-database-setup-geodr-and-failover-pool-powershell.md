---
title: PowerShell の例 - アクティブ geo レプリケーション - プールされた Azure SQL データベース | Microsoft Docs
description: Azure SQL Database のプールされたデータベースに対してアクティブ geo レプリケーションの設定とフェールオーバーを実行する Azure PowerShell のサンプル スクリプト。
services: sql-database
ms.service: sql-database
ms.subservice: high-availability
ms.custom: ''
ms.devlang: PowerShell
ms.topic: sample
author: mashamsft
ms.author: mathoma
ms.reviewer: carlrab
manager: craigg
ms.date: 03/12/2019
ms.openlocfilehash: 737d60d89928bd7ade9aeb9c3aad91dc4e84ab03
ms.sourcegitcommit: 1aefdf876c95bf6c07b12eb8c5fab98e92948000
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66729238"
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-pooled-database-in-azure-sql-database"></a>PowerShell を使用して、Azure SQL Database のプールされたデータベースに対してアクティブ geo レプリケーションを構成する

この PowerShell サンプル スクリプトでは、Azure SQL Database のプールされたデータベースに対してアクティブ geo レプリケーションを構成し、そのデータベースのセカンダリ レプリカにフェールオーバーします。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]
[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

PowerShell をインストールしてローカルで使用する場合、このチュートリアルでは AZ PowerShell 1.4.0 以降が必要になります。 アップグレードする必要がある場合は、[Azure PowerShell モジュールのインストール](/powershell/azure/install-az-ps)に関するページを参照してください。 PowerShell をローカルで実行している場合、`Connect-AzAccount` を実行して Azure との接続を作成することも必要です。

## <a name="sample-scripts"></a>サンプルのスクリプト

[!code-powershell-interactive[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover/setup-geodr-and-failover-elastic-pool.ps1?highlight=17-20 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a>デプロイのクリーンアップ

次のコマンドを使用して、リソース グループと、それに関連付けられているすべてのリソースを削除します。

```powershell
Remove-AzResourceGroup -ResourceGroupName $primaryresourcegroupname
Remove-AzResourceGroup -ResourceGroupName $secondaryresourcegroupname
```

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使用します。 表内の各コマンドは、それぞれのドキュメントにリンクされています。

| command | メモ |
|---|---|
| [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) | すべてのリソースを格納するリソース グループを作成します。 |
| [New-AzSqlServer](/powershell/module/az.sql/new-azsqlserver) | 単一データベースとエラスティック プールをホストする SQL Database サーバーを作成します。 |
| [New-AzSqlElasticPool](/powershell/module/az.sql/new-azsqlelasticpool) | エラスティック プールを作成します。 |
| [New-AzSqlDatabase](/powershell/module/az.sql/new-azsqldatabase) | 単一のデータベースまたはプールされたデータベースを作成します。 |
| [Set-AzSqlDatabase](/powershell/module/az.sql/set-azsqldatabase) | データベースのプロパティを更新するか、エラスティック プールに対して、エラスティック プールから、またはエラスティック プール間でデータベースを移動します。 |
| [New-AzSqlDatabaseSecondary](/powershell/module/az.sql/new-azsqldatabasesecondary)| 既存のデータベースのセカンダリ データベースを作成し、データ レプリケーションを開始します。 |
| [Get-AzSqlDatabase](/powershell/module/az.sql/get-azsqldatabase)| 1 つまたは複数のデータベースを取得します。 |
| [Set-AzSqlDatabaseSecondary](/powershell/module/az.sql/set-azsqldatabasesecondary)| セカンダリ データベースをプライマリに切り替えて、フェールオーバーを開始します。|
| [Get-AzSqlDatabaseReplicationLink](/powershell/module/az.sql/get-azsqldatabasereplicationlink) | Azure SQL Database とリソース グループまたは SQL Server 間の geo レプリケーション リンクを取得します。 |
| [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | 入れ子になったリソースすべてを含むリソース グループを削除します。 |
|||

## <a name="next-steps"></a>次の手順

Azure PowerShell の詳細については、[Azure PowerShell のドキュメント](/powershell/azure/overview)を参照してください。

その他の SQL Database 用の PowerShell サンプル スクリプトは、[Azure SQL Database 用の PowerShell スクリプト](../sql-database-powershell-samples.md)のページにあります。
