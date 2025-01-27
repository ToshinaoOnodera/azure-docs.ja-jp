---
title: メトリック アラートを使用して Azure Automation Runbook を監視する
description: この記事では、メトリックに基づいて Azure Automation Runbook を監視する手順を説明します
services: automation
ms.service: automation
author: georgewallace
ms.author: gwallace
ms.date: 11/01/2018
ms.topic: article
manager: carmonm
ms.openlocfilehash: 7932d057a348957d369ba325044055ac8dfe3428
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "62119896"
---
# <a name="monitoring-runbooks-with-metric-alerts"></a>メトリック アラートによる Runbook の監視

この記事では、Runbook の完了状態に基づいてアラートを作成する方法を説明します。

## <a name="sign-in-to-azure"></a>Azure へのサインイン

https://portal.azure.com で Azure にサインインします

## <a name="create-alert"></a>アラートを作成する

アラートを使うと、監視対象の条件と、その条件が満たされたときに実行するアクションを定義できます。

Azure portal で、Automation アカウントに移動します。 **[監視]** ページで、 **[アラート]** を選び、 **[+ 新しいアラート ルール]** をクリックします。 ターゲットのスコープは、既に Automation アカウントに定義されています。

### <a name="configure-alert-criteria"></a>アラートの条件を構成する

1. **[+ 条件の追加]** をクリックします。 **[シグナルの種類]** で **[メトリック]** を選び、テーブルから **[合計ジョブ数]** を選びます。

2. **[シグナル ロジックの構成]** ページでは、アラートをトリガーするロジックを定義します。 履歴のグラフの下に、 **[Runbook 名]** と **[状態]** の 2 つのディメンションが表示されます。 ディメンションは、結果のフィルター処理に使用できるメトリックのさまざまなプロパティです。 **[Runbook 名]** では、アラート対象の Runbook を選ぶか、空白にままにしてすべての Runbook についてアラートします。 **[状態]** では、監視対象の状態をドロップダウンから選びます。 ドロップダウンに表示される Runbook 名と状態の値は、過去 1 週間に実行したジョブに対するものだけです。

   ドロップダウンに表示されていない状態または Runbook に対するアラートを作成する場合は、ディメンションの横にある **\+** をクリックします。 このアクションによって開くダイアログボックスで、そのディメンションに対して最近生成されなかったカスタム値を入力できます。 プロパティに対して存在しない値を入力すると、アラートはトリガーされません。

   > [!NOTE]
   > **RunbookName** ディメンションに名前を適用しない場合、状態基準を満たす Runbook (隠しシステム Runbook を含む) があると、アラートが表示されます。

3. **[アラート ロジック]** で、アラートの条件としきい値を定義します。 定義した条件のプレビューが下に表示されます。

4. **[評価基準]** で、クエリの対象期間と、クエリの実行頻度を選びます。 たとえば、 **[期間]** で **[直近 5 分]** を選び、 **[頻度]** で **[1 分ごと]** を選ぶと、アラートは、過去 5 分間に条件に一致した Runbook の数を検索します。 このクエリは 1 分ごとに実行し、定義されているアラート条件が 5 分の期間内に見つからなくなると、アラートは自動的に解消されます。 終了したら、 **[完了]** をクリックします。

   ![アラート対象のリソースを選択する](./media/automation-alert-activity-log/configure-signal-logic.png)

### <a name="define-alert-details"></a>アラートの詳細を定義する

1. **[2. アラートの詳細を定義します]** で、アラートのフレンドリ名と説明を入力します。 アラートの条件に一致するように **[重要度]** を設定します。 0 から 4 まで 5 つの重大度レベルがあります。 アラートは重大度とは関係なく同じように処理され、ビジネス ロジックに合わせて重大度を一致させることができます。

1. セクションの下部にあるボタンを使って、完成時にルールを有効にできます。 既定では、ルールは作成時に有効になります。 [いいえ] を選ぶと、**無効**状態でアラートを作成できます。 準備ができたら、Azure Monitor の **[ルール]** ページでルールを選び、 **[有効]** をクリックして有効にします。

### <a name="define-the-action-to-take"></a>実行するアクションを定義する

1. **[3. アクション グループを定義します]** で、 **[+ 新しいアクション グループ]** をクリックします。 アクション グループとは、複数のアラートで使用できるアクションのグループです。 アクションには、電子メール通知、Runbook、webhook などがありますが、これらに限定されるわけではありません。 アクション グループの詳細については、[アクション グループの作成と管理](../azure-monitor/platform/action-groups.md)に関する記事をご覧ください。

1. **[アクション グループ名]** ボックスにフレンドリ名を入力し、短い名前を指定します。 短い名前は、通知がこのグループを使用して送信されるときに長い名前の代わりに使用されます。

1. **[アクション]** セクションの **[アクション タイプ]** で、 **[電子メール/SMS/プッシュ/音声]** を選びます。

1. **[電子メール/SMS/プッシュ/音声]** ページで、名前を指定します。 **[電子メール]** チェック ボックスをオンにし、使用する有効な電子メール アドレスを入力します。

   ![電子メール アクション グループの構成](./media/automation-alert-activity-log/add-action-group.png)

1. **[電子メール/SMS/プッシュ/音声]** ページで **[OK]** をクリックしてページを閉じ、 **[OK]** をクリックして **[アクション グループの追加]** ページを閉じます。 このページで指定した名前が、**アクション名**として保存されます。

1. 完了したら、 **[保存]** をクリックします。 これにより、Runbook が特定の状態で完了するとユーザーにアラートを送るルールが作成されます。

> [!NOTE]
> メール アドレスをアクション グループに追加すると、アドレスがアクション グループに追加されたことを示す通知メールが送信されます。

## <a name="notification"></a>通知

アラートの条件が満たされると、アクション グループは定義されているアクションを実行します。 この記事の例では、メールが送信されます。 次の図は、アラートがトリガーされた後で受け取るメールの例です。

![電子メール アラート](./media/automation-alert-activity-log/alert-email.png)

メトリックが定義されているしきい値を超えなくなると、アラートは非アクティブ化されて、アクション グループは定義されているアクションを実行します。 メール アクションの種類を選択されていると、解消されたことを示す解消メールが送信されます。

## <a name="next-steps"></a>次の手順

Automation アカウントにアラートを統合する他の方法について学習する次の記事に進んでください。

> [!div class="nextstepaction"]
> [Azure Automation Runbook をトリガーするアラートを使用する](automation-create-alert-triggered-runbook.md)
