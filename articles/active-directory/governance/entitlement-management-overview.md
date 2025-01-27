---
title: Azure AD エンタイトルメント管理とは (プレビュー) - Azure Active Directory
description: Azure Active Directory のエンタイトルメント管理と、それを使用してグループ、アプリケーション、SharePoint Online サイトへの内部および外部ユーザーのアクセスを管理する方法の概要を説明します。
services: active-directory
documentationCenter: ''
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.subservice: compliance
ms.date: 05/30/2019
ms.author: rolyon
ms.reviewer: mwahl
ms.collection: M365-identity-device-management
ms.openlocfilehash: efd3ff8a6e7ddf2aa6242cc322d8a6536a6bd26b
ms.sourcegitcommit: cababb51721f6ab6b61dda6d18345514f074fb2e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66474057"
---
# <a name="what-is-azure-ad-entitlement-management-preview"></a>Azure AD エンタイトルメント管理とは (プレビュー)

> [!IMPORTANT]
> Azure Active Directory (Azure AD) のエンタイトルメント管理は現在、パブリック プレビュー段階です。
> このプレビュー バージョンはサービス レベル アグリーメントなしで提供されています。運用環境のワークロードに使用することはお勧めできません。 特定の機能はサポート対象ではなく、機能が制限されることがあります。
> 詳しくは、[Microsoft Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)に関するページをご覧ください。

組織の従業員は、業務を遂行するためにさまざまなグループ、アプリケーション、サイトにアクセスする必要があります。 このアクセスを管理することは困難です。 ほとんどの場合、プロジェクトのためにユーザーに必要なすべてのリソースを整理した一覧はありません。 プロジェクト マネージャーは、必要なリソース、関係する人物、プロジェクトが続く期間をよく理解しています。 ただし、プロジェクト マネージャーには通常、他のユーザーに対してアクセスを承認または許可する権限がありません。 外部の個人または会社と仕事をしようとすると、このシナリオはさらに複雑になります。

Azure Active Directory (Azure AD) のエンタイトルメント管理は、内部ユーザーだけでなく組織外のユーザーを対象に、グループ、アプリケーション、SharePoint Online サイトへのアクセスを管理するために役立ちます。

## <a name="why-use-entitlement-management"></a>エンタイトルメント管理を使用する理由

エンタープライズ組織は、以下のようなリソースへのアクセスを管理する際、しばしば課題に直面します。

- 自分に必要なアクセス権をユーザーが知らない場合がある
- ユーザーが適切な個人またはリソースを探すのが難しい場合がある
- ユーザーがリソースへのアクセス権を見つけて取得した後、業務上の目的に必要な期間よりも長くアクセス権を持ち続ける場合がある

サプライ チェーン組織またはその他のビジネス パートナーに属する外部ユーザーなど、別のディレクトリからアクセスする必要があるユーザーにとっては、これらの問題がいっそう複雑になります。 例:

- 他のディレクトリ内の招待可能な特定の個人全員を、組織があらかじめ把握できていない可能性がある
- 組織がこれらのユーザーを招待できたとしても、ユーザー全員のアクセスを一貫して管理することを組織が忘れてしまう場合がある

Azure AD のエンタイトルメント管理は、これらの課題への対処に役立ちます。

## <a name="what-can-i-do-with-entitlement-management"></a>エンタイトルメント管理では何ができますか?

エンタイトルメント管理の機能の一部を次に示します。

- ユーザーが要求できる関連リソースのパッケージを作成する
- リソースの要求方法と、アクセス期限がいつ切れるかに関する規則を定義する
- 内部ユーザーと外部ユーザー両方のアクセスのライフサイクルを管理する
- リソースの管理を委任する
- 承認者を指名して要求を承認する
- レポートを作成して履歴を追跡する

ID ガバナンスとエンタイトルメント管理の概要については、Ignite 2018 カンファレンスの次のビデオをご覧ください。

>[!VIDEO https://www.youtube.com/embed/aY7A0Br8u5M]

## <a name="what-resources-can-i-manage"></a>どのようなリソースを管理できますか?

エンタイトルメント管理でアクセスを管理できるリソースの種類は次のとおりです。

- Azure AD セキュリティ グループ
- Office 365 グループ
- SaaS アプリケーションや、フェデレーションまたはプロビジョニングをサポートするカスタム統合アプリケーションなどの、Azure AD エンタープライズ アプリケーション
- SharePoint Online サイト コレクションとサイト

Azure AD セキュリティ グループまたは Office 365 グループに依存するその他のリソースへのアクセスを制御することもできます。  例:

- Microsoft Office 365 のライセンスをユーザーに付与するには、アクセス パッケージで Azure AD セキュリティ グループを使用し、そのグループの[グループ ベース ライセンス](../users-groups-roles/licensing-groups-assign.md)を構成します
- Azure リソースを管理するアクセス権をユーザーに付与するには、アクセス パッケージで Azure AD セキュリティ グループを使用し、そのグループの [Azure ロール割り当て](../../role-based-access-control/role-assignments-portal.md)を作成します

## <a name="what-are-access-packages-and-policies"></a>アクセス パッケージとポリシーとは何ですか?

エンタイトルメント管理では、*アクセス パッケージ*の概念を導入しています。 アクセス パッケージは、ユーザーがプロジェクトでの作業や業務の遂行に必要とするすべてのリソースのバンドルです。 リソースには、グループ、アプリケーション、またはサイトへのアクセスが含まれます。 アクセス パッケージは、内部の従業員、さらには組織外のユーザーのアクセスを管理するために使用します。 アクセス パッケージは、*カタログ*と呼ばれるコンテナーに定義されます。

アクセス パッケージには 1 つ以上の*ポリシー*も含まれます。 ポリシーにより、アクセス パッケージにアクセスするための規則またはガードレールを定義します。 ポリシーを有効にすると、適切なユーザーだけが、適切なリソースへのアクセスを、適切な期間に限って許可される体制になります。

![アクセス パッケージとポリシー](./media/entitlement-management-overview/elm-overview-access-package.png)

アクセス パッケージとそのポリシーを使用して、アクセス パッケージ マネージャーは次のものを定義します。

- リソース
- ユーザーがリソースに対して必要とするロール
- アクセスを要求する資格がある内部ユーザーと外部ユーザー
- 承認プロセスと、アクセスを承認または拒否できるユーザー
- ユーザーのアクセス権の継続時間

次の図は、エンタイトルメント管理のさまざまな要素の例を示します。 アクセス パッケージの 2 つの例を示します。

- **アクセス パッケージ 1** には、1 つのグループがリソースとして含まれます。 アクセスは、ディレクトリ内のユーザーの集合がアクセスを要求できるようにするポリシーによって定義されます。
- **アクセス パッケージ 2** には、グループ、アプリケーション、SharePoint Online サイトがリソースとして含まれます。 アクセスは 2 つの異なるポリシーによって定義されます。 最初のポリシーは、ディレクトリ内のユーザーの集合がアクセスを要求できるようにします。 2 番目のポリシーは、外部ディレクトリのユーザーがアクセスを要求できるようにします。

![エンタイトルメント管理の概要](./media/entitlement-management-overview/elm-overview.png)

## <a name="external-users"></a>外部ユーザー

[Azure AD B2B (企業間)](../b2b/what-is-b2b.md) 招待状を使用する場合、自分のリソース ディレクトリに招待して共同作業する外部ゲスト ユーザーの電子メール アドレスをあらかじめ知っている必要があります。 これは、小規模または短期間のプロジェクトで作業していて、すべての参加者を既に知っている場合は効果的ですが、一緒に作業したいユーザーが多い場合や、参加者の入れ替わりがある場合は管理が難しくなります。  たとえば、別の組織と仕事をしていて、その組織との連絡窓口が一本化されていたとしても、時間が経てば、その組織の新たなユーザーもアクセスを必要とするようになるでしょう。

エンタイトルメント管理を使用すれば、同じく Azure AD を使用している、指定した組織のユーザーがアクセス パッケージを要求できるようにするポリシーを定義できます。 承認が必要かどうか、またアクセスの有効期限を指定できます。 承認が必要な場合、以前に招待した外部組織の 1 人以上のユーザーを承認者として指名することもできます。これらのユーザーは、自分の組織のどの外部ユーザーがアクセスを必要としているか、知っている可能性が高いからです。 アクセス パッケージを構成したら、アクセス パッケージへのリンクを外部組織の連絡先の人物に送信できます。 その連絡先は外部組織の他のユーザーと共有することができ、それらのユーザーがこのリンクを使用してアクセス パッケージを要求できます。  その組織に属する、ディレクトリに招待済みのユーザーもそのリンクを使用できます。

要求が承認されると、エンタイトルメント管理は必要なアクセス権をユーザーにプロビジョニングします。これには、ユーザーがまだディレクトリに参加していない場合に、そのユーザーを招待する処理が含まれる場合があります。 Azure AD は、それらのユーザーの B2B アカウントを自動的に作成します。  管理者が以前に、他組織への招待を許可またはブロックする [B2B 許可/拒否リスト](../b2b/allow-deny-list.md)を設定することによって、共同作業を許可する組織を制限していた可能性があることに注意してください。  ユーザーが許可/ブロック リストによって許可されていない場合、そのユーザーは招待されません。

外部ユーザーのアクセスを恒久的にしたくない場合、180 日などの有効期限をポリシーに指定します。 180 日後、アクセス権が更新されない場合、エンタイトルメント管理はそのアクセス パッケージに関連付けられているすべてのアクセス権を削除します。  エンタイトルメント管理によって招待されたユーザーに他のアクセス パッケージが割り当てられていない場合、最後の割り当てを失った時点で、そのユーザーの B2B アカウントは 30 日間サインインできなくなり、その後削除されます。  これにより、不要なアカウントの拡散を防ぎます。  

## <a name="terminology"></a>用語集

エンタイトルメント管理とそのドキュメントについてより深く理解するために、次の用語を確認してください。

| 用語または概念 | 説明 |
| --- | --- |
| エンタイトルメント管理 | アクセス パッケージの割り当て、取り消し、管理を行うサービス。 |
| アクセス パッケージ | ユーザーが要求できるリソースのアクセス許可とポリシーのコレクション。 アクセス パッケージは常にカタログに含まれています。 |
| アクセス要求 | アクセス パッケージへのアクセス要求。 要求は通常、ワークフローを通過します。 |
| policy | ユーザーがアクセスする方法、承認担当者、ユーザーがアクセスできる期間など、アクセスのライフサイクルを定義する一連の規則。 ポリシーの例には、従業員アクセスや外部アクセスがあります。 |
| catalog | 関連リソースとアクセス パッケージのコンテナー。 |
| 一般カタログ | 常に使用できる組み込みのカタログ。 一般カタログにリソースを追加するには、特定のアクセス許可が必要です。 |
| resource | ユーザーがアクセス許可の付与を受けることができる資産またはサービス (グループ、アプリケーション、サイトなど)。 |
| リソースの種類 | グループ、アプリケーション、SharePoint Online サイトを含むリソースの種類。 |
| リソース ロール | リソースに関連付けられているアクセス許可のコレクション。 |
| リソース ディレクトリ | 共有する 1 つ以上のリソースがあるディレクトリ。 |
| 割り当てられたユーザー | ユーザーまたはグループへのアクセス パッケージの割り当て。 |
| enable | アクセス パッケージをユーザーが要求できるようにするプロセス。 |

## <a name="roles-and-permissions"></a>ロールとアクセス許可

エンタイトルメント管理には、職務に応じたさまざまなロールがあります。

| Role | 説明 |
| --- | --- |
| [ユーザー管理者](../users-groups-roles/directory-assign-admin-roles.md#user-administrator) | エンタイトルメント管理のすべての側面を管理します。<br/>ユーザーとグループを作成します。 |
| カタログ作成者 | カタログを作成および管理します。 通常は IT 管理者またはリソース所有者です。 カタログを作成する人物が、自動的にカタログの最初のカタログ所有者になります。 |
| カタログ所有者 | 既存のカタログを編集および管理します。 通常は IT 管理者またはリソース所有者です。 |
| アクセス パッケージ マネージャー | カタログ内のすべての既存アクセス パッケージを編集および管理します。 |
| 承認者 | アクセス パッケージに対する要求を承認します。 |
| 要求元 | アクセス パッケージを要求します。 |

次の表に、これら各ロールのアクセス許可の一覧を示します。

| タスク | ユーザー管理者 | カタログ作成者 | カタログ所有者 | アクセス パッケージ マネージャー | 承認者 |
| --- | :---: | :---: | :---: | :---: | :---: |
| [新しいアクセス パッケージを一般カタログに作成する](entitlement-management-access-package-create.md) | :heavy_check_mark: |  :heavy_check_mark: |  |  |  |
| [新しいアクセス パッケージをカタログに作成する](entitlement-management-access-package-create.md) | :heavy_check_mark: |   | :heavy_check_mark: |  |  |
| [リソース ロールをアクセス パッケージに追加/そこから削除する](entitlement-management-access-package-edit.md) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [アクセス パッケージを要求できるユーザーを指定する](entitlement-management-access-package-edit.md#add-a-new-policy) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [アクセス パッケージにユーザーを直接割り当てる](entitlement-management-access-package-edit.md#directly-assign-a-user) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [アクセス パッケージに割り当てられているユーザーを表示する](entitlement-management-access-package-edit.md#view-who-has-an-assignment) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [アクセス パッケージの要求を表示する](entitlement-management-access-package-edit.md#view-requests) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [要求の配信エラーを表示する](entitlement-management-access-package-edit.md#view-a-requests-delivery-errors) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [保留中の要求をキャンセルする](entitlement-management-access-package-edit.md#cancel-a-pending-request) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [アクセス パッケージを非表示にする](entitlement-management-access-package-edit.md#change-the-hidden-setting) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [アクセス パッケージを削除する](entitlement-management-access-package-edit.md#delete) | :heavy_check_mark: |  | :heavy_check_mark: | :heavy_check_mark: |  |
| [アクセス要求を承認する](entitlement-management-request-approve.md) |  |  |  |  | :heavy_check_mark: |
| [カタログを作成する](entitlement-management-catalog-create.md) | :heavy_check_mark: | :heavy_check_mark: |  |  |  |
| [リソースを全般カタログに追加/そこから削除する](entitlement-management-catalog-create.md#add-resources-to-a-catalog) | :heavy_check_mark: |  |  |  |  |
| [リソースをカタログに追加/そこから削除する](entitlement-management-catalog-create.md#add-resources-to-a-catalog) | :heavy_check_mark: |  | :heavy_check_mark: |  |  |
| [カタログ所有者またはアクセス パッケージ マネージャーを追加する](entitlement-management-catalog-create.md#add-catalog-owners-or-access-package-managers) | :heavy_check_mark: |  | :heavy_check_mark: |  |  |
| [カタログを編集/削除する](entitlement-management-catalog-create.md#edit-a-catalog) | :heavy_check_mark: |  | :heavy_check_mark: |  |  |

## <a name="license-requirements"></a>ライセンスの要件

[!INCLUDE [Azure AD Premium P2 license](../../../includes/active-directory-p2-license.md)]

Azure Government、Azure Germany、Azure China 21Vianet などの特殊なクラウドは現在、このプレビューではご利用いただけません。

## <a name="next-steps"></a>次の手順

- [チュートリアル:最初のアクセス パッケージを作成する](entitlement-management-access-package-first.md)
- [一般的なシナリオ](entitlement-management-scenarios.md)
