---
title: Azure CLI を使用した Azure リソースの管理 | Microsoft Docs
description: Azure CLI と Azure Resource Manager を使用してリソースを管理します。
services: azure-resource-manager
documentationcenter: ''
author: mumian
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 02/11/2019
ms.author: jgao
ms.openlocfilehash: 076c57f5415a4f6f19252fb5a3546e5e9a8a23f4
ms.sourcegitcommit: 41ca82b5f95d2e07b0c7f9025b912daf0ab21909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "60550245"
---
# <a name="manage-azure-resources-by-using-azure-cli"></a>Azure CLI を使用した Azure リソースの管理

[Azure Resource Manager](resource-group-overview.md) と共に Azure CLI を使用して Azure リソースを管理する方法について説明します。 リソース グループの管理については、「[Manage Azure resource groups by using Azure CLI (Azure CLI を使用した Azure リソース グループの管理)](./manage-resource-groups-cli.md)」をご覧ください。

リソースの管理に関するその他の記事:

- 「[Manage Azure resources by using the Azure portal (Azure portal を使用した Azure リソースの管理)](./manage-resources-portal.md)」
- 「[Azure PowerShell を使用した Azure リソースの管理](./manage-resources-powershell.md)」

## <a name="deploy-resources-to-an-existing-resource-group"></a>リソースを既存のリソース グループにデプロイする

Azure PowerShell を使用して直接 Azure リソースをデプロイするか、または Azure リソースを作成する Resource Manager テンプレートをデプロイできます。

### <a name="deploy-a-resource"></a>リソースのデプロイ

次のスクリプトでは、ストレージ アカウントを作成します。

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
echo "Enter the location (i.e. centralus):" &&
read location &&
echo "Enter the storage account name:" &&
read storageAccountName &&
az storage account create --resource-group $resourceGroupName --name $storageAccountName --location $location --sku Standard_LRS --kind StorageV2 &&
az storage account show --resource-group $resourceGroupName --name $storageAccountName 
```

### <a name="deploy-a-template"></a>テンプレートのデプロイ

次のスクリプトでは、ストレージ アカウントを作成するためのクイックスタート テンプレートをデプロイします。 詳細については、「[クイック スタート: Visual Studio Code を使って Azure Resource Manager テンプレートを作成する](./resource-manager-quickstart-create-templates-use-visual-studio-code.md?tabs=PowerShell)」をご覧ください。

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
echo "Enter the location (i.e. centralus):" &&
read location &&
az group deployment create --resource-group $resourceGroupName --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json"
```

詳細については、「[Deploy resources with Resource Manager templates and Azure CLI](./resource-group-template-deploy-cli.md)」 (Resource Manager テンプレートと Azure CLI を使用したリソースのデプロイ) を参照してください。

## <a name="deploy-a-resource-group-and-resources"></a>リソース グループとリソースをデプロイする

リソース グループを作成して、リソースをそのグループにデプロイすることができます。 詳しくは、「[リソース グループを作成してリソースをデプロイする](./deploy-to-subscription.md#create-resource-group-and-deploy-resources)」をご覧ください。

## <a name="deploy-resources-to-multiple-subscriptions-or-resource-groups"></a>複数のサブスクリプションまたはリソース グループにリソースをデプロイする

テンプレートに含まれているリソースはすべて 1 つのリソース グループにデプロイするのが一般的です。 一方、さまざまなリソースを 1 つにまとめたうえで、複数のリソース グループまたはサブスクリプションにデプロイしたい状況もあります。 詳しくは、「[複数のサブスクリプションまたはリソース グループに Azure リソースをデプロイする](./resource-manager-cross-resource-group-deployment.md)」をご覧ください。

## <a name="delete-resources"></a>リソースを削除する

次のスクリプトは、ストレージ アカウントを削除する方法を示しています。

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
echo "Enter the storage account name:" &&
read storageAccountName &&
az storage account delete --resource-group $resourceGroupName --name $storageAccountName 
```

Azure Resource Manager によるリソースの削除順序の決定方法について詳しくは、「[Azure Resource Manager によるリソース グループの削除](./resource-group-delete.md)」をご覧ください。

## <a name="move-resources"></a>リソースの移動

次のスクリプトは、1 つのリソース グループからストレージ アカウントを削除して別のリソース グループに移動する方法を示しています。

```azurecli-interactive
echo "Enter the source Resource Group name:" &&
read srcResourceGroupName &&
echo "Enter the destination Resource Group name:" &&
read destResourceGroupName &&
echo "Enter the storage account name:" &&
read storageAccountName &&
storageAccount=$(az resource show --resource-group $srcResourceGroupName --name $storageAccountName --resource-type Microsoft.Storage/storageAccounts --query id --output tsv) &&
az resource move --destination-group $destResourceGroupName --ids $storageAccount
```

詳細については、「 [新しいリソース グループまたはサブスクリプションへのリソースの移動](resource-group-move-resources.md)」を参照してください。

## <a name="lock-resources"></a>リソースのロック

ロックすることで、組織内の他のユーザーが重要なリソース (Azure サブスクリプション、リソース グループ、リソースなど) を誤って削除または変更することを防ぎます。 

次のスクリプトでは、アカウントを削除できないように、ストレージ アカウントをロックします。

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
echo "Enter the storage account name:" &&
read storageAccountName &&
az lock create --name LockSite --lock-type CanNotDelete --resource-group $resourceGroupName --resource-name $storageAccountName --resource-type Microsoft.Storage/storageAccounts 
```

次のスクリプトでは、ストレージ アカウントのすべてのロックを取得します。

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
echo "Enter the storage account name:" &&
read storageAccountName &&
az lock list --resource-group $resourceGroupName --resource-name $storageAccountName --resource-type Microsoft.Storage/storageAccounts --parent ""
```

次のスクリプトでは、ストレージ アカウントのロックを削除します。

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
echo "Enter the storage account name:" &&
read storageAccountName &&
lockId=$(az lock show --name LockSite --resource-group $resourceGroupName --resource-type Microsoft.Storage/storageAccounts --resource-name $storageAccountName --output tsv --query id)&&
az lock delete --ids $lockId
```

詳細については、[「Azure Resource Manager によるリソースのロック」](resource-group-lock-resources.md)を参照してください。

## <a name="tag-resources"></a>リソースへのタグ付け

タグ付けすると、リソース グループとリソースを論理的に整理できます。 詳しくは、「[タグを使用した Azure リソースの整理](./resource-group-using-tags.md#azure-cli)」をご覧ください。

## <a name="manage-access-to-resources"></a>リソースへのアクセスの管理

[ロールベースのアクセス制御 (RBAC)](../role-based-access-control/overview.md) は、Azure に存在するリソースに対するアクセス権を管理するための手法です。 詳しくは、[RBAC と Azure CLI を使用したアクセスの管理](../role-based-access-control/role-assignments-cli.md)に関する記事をご覧ください。

## <a name="next-steps"></a>次の手順

- Azure Resource Manager については、「[Azure Resource Manager の概要](./resource-group-overview.md)」を参照してください。
- Resource Manager テンプレートの構文については、「[Azure Resource Manager テンプレートの構造と構文の詳細](./resource-group-authoring-templates.md)」を参照してください。
- テンプレートを開発する方法については、[ステップバイステップのチュートリアル](/azure/azure-resource-manager/)のページをご覧ください。
- Azure Resource Manager テンプレートのスキーマを表示するには、[テンプレート リファレンス](/azure/templates/)のページをご覧ください。
