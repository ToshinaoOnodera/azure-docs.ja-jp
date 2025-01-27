---
author: vladvino
ms.service: api-management
ms.topic: include
ms.date: 11/09/2018
ms.author: vlvinogr
ms.openlocfilehash: 2bfa356deeede1c16bd5a464ea7081132a67faf6
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66238126"
---
## <a name="append-other-apis"></a>その他の API の追加

API は、OpenAPI Specification、SOAP API、Azure App Service の API Apps 機能、Azure Function App、Azure Logic Apps、Azure Service Fabric を含む、別のサービスで公開されている API によって構成される場合があります。

![API のインポート](./media/api-management-append-apis/import.png)

既存の API に別の API を追加するには、次の手順を実行します。 別の API をインポートすると、操作が現在の API に追加されます。

1. Azure portal で Azure API Management インスタンスに移動します。
2. 左にあるメニューから **[API]** を選択します。
3. 別の API を追加する API の隣の **[...]** をクリックします。
4. ドロップダウン メニューから **[インポート]** を選択します。
5. API のインポート元のサービスを選択します。