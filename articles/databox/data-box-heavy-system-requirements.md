---
title: Microsoft Azure Data Box Heavy のシステム要件 | Microsoft Docs
description: Azure Data Box Heavy のソフトウェア要件とネットワーク要件について説明します
services: databox
author: alkohli
ms.service: databox
ms.subservice: heavy
ms.topic: article
ms.date: 05/22/2019
ms.author: alkohli
ms.openlocfilehash: b9e249885bd0e930773d4b374f85d72e60abdbdc
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "66427745"
---
# <a name="azure-data-box-heavy-system-requirements-preview"></a>Azure Data Box Heavy のシステム要件 (プレビュー)

この記事では、Azure Data Box Heavy デバイスとそのデバイスに接続するクライアントの重要なシステム要件について説明します。 この情報は、Data Box Heavy をデプロイする前によく確認し、デプロイ時やそれ以降の操作時にも、必要に応じて繰り返し参照することをお勧めします。

システム要件は次のとおりです。

* **Data Box Heavy に接続するホストのソフトウェア要件** - サポートされているプラットフォーム、ローカル Web UI 用のブラウザー、SMB クライアント、および Data Box に接続できるホストのその他の要件について説明します。
* **Data Box Heavy のネットワーク要件** - Data Box Heavy デバイスの最適な操作のためのネットワーク要件についての情報を示します。

## <a name="software-requirements"></a>ソフトウェア要件

ソフトウェア要件には、サポートされるオペレーティング システム、ローカル Web UI でサポートされるブラウザー、および SMB クライアントに関する情報が含まれます。

### <a name="supported-operating-systems-for-clients"></a>クライアントでサポートされるオペレーティング システム

[!INCLUDE [data-box-supported-os-clients](../../includes/data-box-supported-os-clients.md)]

### <a name="supported-file-systems-for-linux-clients"></a>Linux クライアントでサポートされるファイル システム

[!INCLUDE [data-box-supported-file-systems-clients](../../includes/data-box-supported-file-systems-clients.md)]

### <a name="supported-storage-accounts"></a>サポートされるストレージ アカウント

[!INCLUDE [data-box-supported-storage-accounts](../../includes/data-box-supported-storage-accounts.md)]

### <a name="supported-storage-types"></a>サポートされるストレージの種類

[!INCLUDE [data-box-supported-storage-types](../../includes/data-box-supported-storage-types.md)]

### <a name="supported-web-browsers"></a>サポートされている Web ブラウザー

[!INCLUDE [data-box-supported-web-browsers](../../includes/data-box-supported-web-browsers.md)]

## <a name="networking-requirements"></a>ネットワーク要件

お客様のデータセンターには、高速ネットワークが必要です。 最速のコピー速度を得るため、2 つの 40 GbE 接続 (ノードごとに 1 つずつ) を並列で利用できます。 40 GbE を使用できない場合は、少なくとも 2 つの 10 GbE 接続 (ノードごとに 1 つずつ) を使用することをお勧めします。

## <a name="next-steps"></a>次の手順

* [Azure Data Box をデプロイする](data-box-deploy-ordered.md)
