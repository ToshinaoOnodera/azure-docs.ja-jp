---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 09/04/2018
ms.author: glenga
ms.openlocfilehash: c20f86fe7fdcfc7ecc940923a8c98fa1fbf4cf65
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66132187"
---
## <a name="create-a-resource-group"></a>リソース グループの作成

[az group create](/cli/azure/group) でリソース グループを作成します。 Azure リソース グループとは、Function App、データベース、ストレージ アカウントなどの Azure リソースのデプロイと管理に使用する論理コンテナーです。

次の例では、`myResourceGroup` という名前のリソース グループを作成します。  
Cloud Shell を使用していない場合は、まず `az login` でサインインします。

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```
通常は、現在地付近の地域にリソース グループおよびリソースを作成します。 App Service プランがサポートされているすべての場所を表示するには、[az appservice list-locations](/cli/azure/appservice#az-appservice-list-locations) コマンドを実行します。
