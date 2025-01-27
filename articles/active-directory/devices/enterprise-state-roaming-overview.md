---
title: Azure Active Directory の Enterprise State Roaming とは | Microsoft Docs
description: Windows デバイスの Enterprise State Roaming の設定について取り上げます。 Enterprise State Roaming によって複数の Windows デバイスの使用環境が統一され、新しいデバイスを構成するために必要な時間が短縮されます。
services: active-directory
keywords: Enterprise State Roaming とは, エンタープライズ同期, Windows クラウド
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: daveba
editor: curtand
ms.subservice: devices
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2018
ms.author: joflore
ms.collection: M365-identity-device-management
ms.openlocfilehash: d3a2a81bd8aa3fc99d033564e8a8782c79261305
ms.sourcegitcommit: 41ca82b5f95d2e07b0c7f9025b912daf0ab21909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "60353144"
---
# <a name="what-is-enterprise-state-roaming"></a>Enterprise State Roaming とは

Windows 10 では、 [Azure Active Directory (Azure AD)](../fundamentals/active-directory-whatis.md) のユーザーが、そのユーザー設定とアプリケーション設定のデータをクラウドと安全に同期させることができます。 Enterprise State Roaming によって複数の Windows デバイスの使用環境が統一され、新しいデバイスを構成するために必要な時間が短縮されます。 Enterprise State Roaming の働きは、Windows 8 で初めて導入された標準的な [コンシューマー設定の同期機能](https://go.microsoft.com/fwlink/?linkid=2015135) と似ています。 それに加えて、Enterprise State Roaming には次の機能が用意されています。

* **企業データとコンシューマー データの分離 – 組織**のデータはその組織の管理下に置かれます。コンシューマー クラウド アカウントに企業データが混入したり、エンタープライズ クラウド アカウントにコンシューマー データが混入したりすることはありません。
* **セキュリティの強化** – データはユーザーの Windows 10 デバイスから送信される前に、Azure Rights Management (Azure RMS) を使って自動的に暗号化されます。クラウドには、暗号化された状態のままデータが保存されます。 名前空間 (設定の名前や Windows アプリの名前) を除き、コンテンツはすべて暗号化された状態でクラウドに保存されます。  
* **管理と監視の向上** – Azure AD ポータルの統合により、組織内のだれがどのデバイスの設定を同期させているかを管理および表示できます。 

複数の Azure リージョンで Enterprise State Roaming を使用できます。 利用できるリージョンの更新された一覧については、Azure Active Directory の [リージョン別の Azure サービス](https://azure.microsoft.com/regions/#services) に関するページをご覧ください。

| 記事 | 説明 |
| --- | --- |
| [Azure Active Directory の Enterprise State Roaming を有効にする](enterprise-state-roaming-enable.md) |Enterprise State Roaming は、Azure Active Directory (Azure AD) の Premium サブスクリプションを所有しているすべての組織が利用できます。 Azure AD サブスクリプションの取得方法について詳しくは、 [Azure AD の製品ページ](https://azure.microsoft.com/services/active-directory) を参照してください。 |
| [設定とデータのローミングに関する FAQ](enterprise-state-roaming-faqs.md) |このトピックでは、設定とアプリ データの同期に関する質問とその答えを IT 管理者向けに紹介しています。 |
| [設定を同期させるためのグループ ポリシーと MDM の設定](enterprise-state-roaming-group-policy-settings.md) |Windows 10 では、グループ ポリシーとモバイル デバイス管理 (MDM) のポリシー設定を通じて、設定の同期を制限することができます。 |
| [Windows 10 ローミング設定リファレンス](enterprise-state-roaming-windows-settings-reference.md) |Windows 10 でローミングまたはバックアップされる全設定の一覧が掲載されています。 |
| [トラブルシューティング](enterprise-state-roaming-troubleshooting.md) |このトピックでは、トラブルシューティングの基本的な手順について説明します。既知の問題の一覧も含まれています。 |

## <a name="next-steps"></a>次の手順

Enterprise State Roaming を有効にする方法については、「[Enterprise State Roaming を有効にする](enterprise-state-roaming-enable.md)」を参照してください。
