---
title: Azure メディア リソースを Azure Germany からグローバル Azure に移行する
description: この記事では、Azure メディア リソースの Azure Germany からグローバル Azure への移行に関する情報を提供します。
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 08/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 9c1426391edb42ecc3e74ee84649bb69196c45dd
ms.sourcegitcommit: 41ca82b5f95d2e07b0c7f9025b912daf0ab21909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "60686335"
---
# <a name="migrate-media-resources-to-global-azure"></a>メディア リソースをグローバル Azure に移行する

この記事には、Azure メディア リソースの Azure Germany からグローバル Azure への移行に役立つ可能性のある情報が含まれています。

## <a name="media-services"></a>Media Services

Azure Media Services では、独自のストレージ アカウントとすべてのメディア資産を構成します。 まず、グローバル Azure で新しい Media Services アカウントを作成します。 次に、対応するメディア成果物を再読み込みし、新しい Media Services アカウントでエンコードとストリーミングを実行します。

詳細:

- [Media Services のチュートリアル](https://docs.microsoft.com/azure/media-services/#step-by-step-tutorials)を完了することによって知識を更新します。
- [Media Services の概要](../media-services/previous/media-services-overview.md)を確認します。
- [Media Services アカウントを作成する](../media-services/previous/media-services-portal-create-account.md)方法を確認します。

## <a name="media-player"></a>Media Player

Azure Media Player では、複数のエンドポイントを選択できます。 Azure Germany エンドポイントまたはグローバル Azure エンドポイントからコンテンツをストリーミングできます。

詳しくは、[Azure Media Player](https://ampdemo.azureedge.net/azuremediaplayer.html) をご覧ください。

## <a name="next-steps"></a>次の手順

次のサービス カテゴリのリソースを移行するためのツール、テクニック、および推奨事項について学習します。

- [Compute](./germany-migration-compute.md)
- [ネットワーク](./germany-migration-networking.md)
- [Storage](./germany-migration-storage.md)
- [Web](./germany-migration-web.md)
- [データベース](./germany-migration-databases.md)
- [Analytics](./germany-migration-analytics.md)
- [IoT](./germany-migration-iot.md)
- [統合](./germany-migration-integration.md)
- [ID](./germany-migration-identity.md)
- [セキュリティ](./germany-migration-security.md)
- [管理ツール](./germany-migration-management-tools.md)
