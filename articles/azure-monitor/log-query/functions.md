---
title: Azure Monitor ログ クエリの関数 | Microsoft Docs
description: この記事では、Azure Monitor で関数を使用して、あるクエリを別のログ クエリから呼び出す方法について説明します。
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 11/15/2018
ms.author: bwren
ms.openlocfilehash: 7eb5f090026b415e3c980116a9317594f4ca8115
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "60728068"
---
# <a name="using-functions-in-azure-monitor-log-queries"></a>Azure Monitor ログ クエリでの関数の使用

> [!NOTE]
> このレッスンを完了する前に、[Analytics ポータルの概要](get-started-portal.md)および[クエリの概要](get-started-queries.md)に関するチュートリアルを完了する必要があります。

[!INCLUDE [log-analytics-demo-environment](../../../includes/log-analytics-demo-environment.md)]


ログ クエリは、別のクエリで使用するために関数として保存できます。 これにより、複雑なクエリを複数のパーツに分割することで単純化でき、共通のコードを複数のクエリで再利用できます。

## <a name="create-a-function"></a>関数を作成する

Azure portal の Log Analytics で **[保存]** をクリックした後、次の表の情報を指定して関数を作成します。

| Setting | 説明 |
|:---|:---|
| Name           | **クエリ エクスプローラー**に表示されるクエリの名前。 |
| 名前を付けて保存        | Function |
| 関数のエイリアス | この関数を他のクエリの中で使用するための短い名前。 スペースを含めることはできず、一意である必要があります。 |
| Category       | 保存したクエリと関数を**クエリ エクスプローラー**内で整理するためのカテゴリ。 |

> [!NOTE]
> Azure Monitor 内の関数に、別の関数を含めることはできません。

> [!NOTE]
> Azure Monitor ログ クエリに関数を保存することは可能ですが、現時点で、Application Insights クエリには保存できません。



## <a name="use-a-function"></a>関数を使用する
関数は、そのエイリアスを別のクエリに含めることによって使用します。 それは他のテーブルと同じように使用できます。

## <a name="example"></a>例
次のサンプル クエリでは、最終日に報告された、更新されていないセキュリティ更新プログラムが返されます。 このクエリを、_security_updates_last_day_ というエイリアスを持つ関数として保存します。 

```Kusto
Update
| where TimeGenerated > ago(1d) 
| where Classification == "Security Updates" 
| where UpdateState == "Needed"
```

別のクエリを作成し、_security_updates_last_day_ 関数を参照して、SQL に関連する更新が必要なセキュリティ更新プログラムを検索します。

```Kusto
security_updates_last_day | where Title contains "SQL"
```

## <a name="next-steps"></a>次の手順
Azure Monitor ログ クエリの記述に関するその他のレッスンを参照してください。

- [文字列操作](string-operations.md)
- [日付と時刻の操作](datetime-operations.md)
- [集計関数](aggregations.md)
- [高度な集計](advanced-aggregations.md)
- [JSON とデータ構造](json-data-structures.md)
- [結合](joins.md)
- [グラフ](charts.md)
