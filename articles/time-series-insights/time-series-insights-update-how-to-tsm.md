---
title: Azure Time Series Insights プレビューでのデータ モデリング | Microsoft Docs
description: Azure Time Series Insights プレビューでのデータ モデリングについて説明します。
author: ashannon7
ms.author: dpalled
ms.workload: big-data
manager: cshankar
ms.service: time-series-insights
services: time-series-insights
ms.topic: conceptual
ms.date: 05/07/2019
ms.custom: seodec18
ms.openlocfilehash: 73384868deb8f0e33b233e363c42a12adbcbe402
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "66237562"
---
# <a name="data-modeling-in-azure-time-series-insights-preview"></a>Azure Time Series Insights プレビューでのデータ モデリング

このドキュメントでは、Azure Time Series Insights プレビューに従ってタイム シリーズ モデルを操作する方法について説明します。 いくつかの一般的なデータ シナリオについて詳しく説明します。

更新を使用する方法の詳細については、「[Azure Time Series Insights Preview explorer](./time-series-insights-update-explorer.md)」(Azure Time Series Insights プレビュー エクスプローラー) をご覧ください。

## <a name="types"></a>型

### <a name="create-a-single-type"></a>1 つの種類を作成する

1. タイム シリーズ モデル セレクター パネルに移動し、メニューから **[種類]** を選択します。 パネルを折りたたんで、タイム シリーズ モデルの種類に注目します。

    [![1 つの種類を作成する](media/v2-update-how-to-tsm/portal_one.png)](media/v2-update-how-to-tsm/portal_one.png#lightbox)

1. **[追加]** を選択します。
1. 種類に関係するすべての詳細情報を入力して、 **[作成]** を選択します。 この操作により、環境に種類が作成されます。

    [![種類を追加する](media/v2-update-how-to-tsm/portal_two.png)](media/v2-update-how-to-tsm/portal_two.png#lightbox)

### <a name="bulk-upload-one-or-more-types"></a>1 つまたは複数の種類を一括アップロードする

1. **[JSON をアップロードします]** を選択します。
1. 種類のペイロードを含むファイルを選択します。
1. **[アップロード]** を選択します。

    [![JSON をアップロードする](media/v2-update-how-to-tsm/portal_three.png)](media/v2-update-how-to-tsm/portal_three.png#lightbox)

### <a name="edit-a-single-type"></a>1 つの種類を編集する

1. 種類を選択して、 **[編集]** を選択します。 
1. 必要な変更を行い、 **[保存]** を選択します。

    [![種類を編集する](media/v2-update-how-to-tsm/portal_four.png)](media/v2-update-how-to-tsm/portal_four.png#lightbox)

### <a name="delete-a-type"></a>種類を削除する

1. 種類を選択して、 **[削除]** を選択します。
1. 種類にインスタンスが関連付けられていない場合は、削除されます。

    [![種類を削除する](media/v2-update-how-to-tsm/portal_five.png)](media/v2-update-how-to-tsm/portal_five.png#lightbox)

## <a name="hierarchies"></a>階層

### <a name="create-a-single-hierarchy"></a>1 つの階層を作成する

1. タイム シリーズ モデル セレクター パネルに移動し、メニューから **[階層]** を選択します。 パネルを折りたたんで、タイム シリーズ モデルの階層に注目します。

    [![階層を選択する](media/v2-update-how-to-tsm/portal_six.png)](media/v2-update-how-to-tsm/portal_six.png#lightbox)

1. **[追加]** を選択します。

    [![階層を追加する](media/v2-update-how-to-tsm/portal_seven.png)](media/v2-update-how-to-tsm/portal_seven.png#lightbox)

1. 右側のウィンドウで **[レベルの追加]** を選択します。

    [![レベルを追加する](media/v2-update-how-to-tsm/portal_eight.png)](media/v2-update-how-to-tsm/portal_eight.png#lightbox)

1. 階層の詳細を入力して、 **[作成]** を選択します。

    [![レベルを作成する](media/v2-update-how-to-tsm/portal_nine.png)](media/v2-update-how-to-tsm/portal_nine.png#lightbox)

### <a name="bulk-upload-one-or-more-hierarchies"></a>1 つまたは複数の階層を一括アップロードする

1. **[JSON をアップロードします]** を選択します。
1. 階層のペイロードを含むファイルを選択します。
1. **[アップロード]** を選択します。

    [![階層を一括アップロードする](media/v2-update-how-to-tsm/portal_ten.png)](media/v2-update-how-to-tsm/portal_ten.png#lightbox)

### <a name="edit-a-single-hierarchy"></a>1 つの階層を編集する

1. 階層を選択し、 **[編集]** を選択します。
1. 必要な変更を行い、 **[保存]** を選択します。

    [![1 つの階層を編集する](media/v2-update-how-to-tsm/portal_eleven.png)](media/v2-update-how-to-tsm/portal_eleven.png#lightbox)

### <a name="delete-a-hierarchy"></a>階層を削除する

1. 階層を選択し、 **[削除]** を選択します。 
1. 階層にインスタンスが関連付けられていない場合は、削除されます。

    [![階層を削除する](media/v2-update-how-to-tsm/portal_twelve.png)](media/v2-update-how-to-tsm/portal_twelve.png#lightbox)

## <a name="instances"></a>Instances

### <a name="create-a-single-instance"></a>1 つのインスタンスを作成する

1. タイム シリーズ モデル セレクター パネルに移動し、メニューから **[インスタンス]** を選択します。 パネルを折りたたんで、タイム シリーズ モデルのインスタンスに注目します。

    [![1 つのインスタンスを作成する](media/v2-update-how-to-tsm/portal_thirteen.png)](media/v2-update-how-to-tsm/portal_thirteen.png#lightbox)

1. **[追加]** を選択します。

    [![インスタンスを追加する](media/v2-update-how-to-tsm/portal_fourteen.png)](media/v2-update-how-to-tsm/portal_fourteen.png#lightbox)

1. インスタンスの詳細を入力し、種類と階層の関連付けを選択して、 **[作成]** を選択します。

### <a name="bulk-upload-one-or-more-instances"></a>1 つまたは複数のインスタンスを一括アップロードする

1. **[JSON をアップロードします]** を選択します。
1. インスタンスのペイロードを含むファイルを選択します。

    [![1 つまたは複数のインスタンスを一括アップロードする](media/v2-update-how-to-tsm/portal_fifteen.png)](media/v2-update-how-to-tsm/portal_fifteen.png#lightbox)

1. **[アップロード]** を選択します。

### <a name="edit-a-single-instance"></a>1 つのインスタンスを編集する

1. インスタンスを選択して、 **[編集]** を選択します。 
1. 必要な変更を行い、 **[保存]** を選択します。

    [![1 つのインスタンスを編集する](media/v2-update-how-to-tsm/portal_sixteen.png)](media/v2-update-how-to-tsm/portal_sixteen.png#lightbox)

## <a name="next-steps"></a>次の手順

- タイム シリーズ モデルの詳細については、「[Data modeling](./time-series-insights-update-tsm.md)」(データ モデリング) をご覧ください。

- プレビューの詳細については、「[Visualize data in the Azure Time Series Insights Preview explorer](./time-series-insights-update-explorer.md)」(Azure Time Series Insights プレビュー エクスプローラーでデータを視覚化する) をご覧ください。

- サポートされている JSON の構造の詳細については、「[サポートされている JSON 構造](./time-series-insights-send-events.md#json)」をご覧ください。
