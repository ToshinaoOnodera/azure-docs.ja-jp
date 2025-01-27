---
title: ナレッジ ベースを作成する
titleSuffix: QnA Maker API - Azure Cognitive Services
description: QnA Maker API サービス ポータルを使用して、おしゃべり機能を備えるナレッジ ベースを作成します。 これにより、アプリが魅力的になります。 上位の事前設定済みのおしゃべりのセットをボットのおしゃべりの開始点として KB に追加すると、最初から作成するよりもコストと時間を節約することができます。
services: cognitive-services
author: tulasim88
manager: nitinme
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: article
ms.date: 05/10/2019
ms.author: tulasim
ms.custom: seodec18
ms.openlocfilehash: 6b64315d8639cf8a7204ee809598567ec76fd188
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "65541796"
---
# <a name="quickstart-create-a-knowledge-base-using-the-qna-maker-api-service-portal"></a>クイック スタート:QnA Maker API サービス ポータルを使用してナレッジ ベースを作成する

QnA Maker API サービス ポータルでは、ナレッジ ベースを作成するときに既存のデータ ソースを簡単に追加できます。 次のドキュメントの種類から、新しい QnA Maker ナレッジ ベースを作成できます。

<!-- added for scanability -->
* FAQ ページ
* 製品マニュアル
* 構造化ドキュメント

おしゃべりのパーソナリティを含めて、ユーザーを引き付けるナレッジにします。

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) を作成してください。 

## <a name="create-a-new-knowledge-base"></a>新しいナレッジ ベースの作成

1. Azure 資格情報で [QnA Maker ポータル](https://qnamaker.ai)にサインインし、 **[Create a knowledge base]** を選択します。

1. QnA Maker サービスをまだ作成していない場合、 **[Create a QnA service]\(QnA サービスの作成\)** を選択します。 

1. QnA Maker ポータルの**手順 2** のリストから、QnA Maker サービスと関連付けられた Azure テナント、Azure サブスクリプション名、および Azure リソース名を選択します。 ナレッジ ベースをホストする Azure QnA Maker サービスを選択します。

    ![QnA サービスのセットアップ](../media/qnamaker-how-to-create-kb/setup-qna-resource.png)

1. ナレッジ ベースの名前と、新しいナレッジ ベースのデータ ソースを入力します。

    ![データ ソースの設定](../media/qnamaker-how-to-create-kb/set-data-sources.png)

    - サービスに**名前**を付けます。 重複した名前と特殊文字がサポートされています。
    - 抽出するデータの URL を追加します。 サポートされているソースの種類については[こちら](../Concepts/data-sources-supported.md)をご覧ください。
    - 抽出するデータのファイルをアップロードします。 追加できるドキュメントの数については、[価格情報](https://aka.ms/qnamaker-pricing)をご覧ください。
    - QnA を手動で追加する場合、上の図に示した**手順 4** は省略できます。

1. **おしゃべり**を KB に追加します。 いずれかのパーソナリティを選択して、おしゃべりのサポートをボットに追加します。 

    ![おしゃべりを KB に追加する](../media/qnamaker-how-to-create-kb/create-kb-chit-chat.png)

1. **[Create your KB]\(KB の作成\)** を選択します。

    ![KB の作成](../media/qnamaker-how-to-create-kb/create-kb.png)

1. データが抽出されるまで数分かかります。

    ![抽出](../media/qnamaker-how-to-create-kb/hang-tight-extraction.png)

1. ナレッジ ベースが正常に作成されると、**ナレッジ ベース** ページにリダイレクトされます。

## <a name="clean-up-resources"></a>リソースのクリーンアップ

ナレッジ ベースを作成できたら、QnA Maker ポータルで削除します。

## <a name="next-steps"></a>次の手順

コスト削減対策として、QnA Maker 用に作成する Azure リソースのすべてではなく、一部を[共有](upgrade-qnamaker-service.md?#share-existing-services-with-qna-maker)することができます。

> [!div class="nextstepaction"]
> [Add chit-chat personal](./chit-chat-knowledge-base.md)\(おしゃべり個人の追加\)
