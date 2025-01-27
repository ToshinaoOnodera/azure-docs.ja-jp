---
title: インクルード ファイル
description: インクルード ファイル
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 04/04/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: d35da4f1eaed91411c015ed7665944d886f9d79c
ms.sourcegitcommit: 3e98da33c41a7bbd724f644ce7dedee169eb5028
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67181030"
---
Azure Portal を使用して Resource Manager デプロイ モデルで VNet を作成するには、次の手順に従います。 これらの手順をチュートリアルとして使用する場合は、[例として示されている値](#values)を使用してください。 これらの手順をチュートリアルとして使用しない場合は、必ず独自の値に置き換えてください。 仮想ネットワークの操作の詳細については、「 [仮想ネットワークの概要](../articles/virtual-network/virtual-networks-overview.md)」を参照してください。

>[!NOTE]
>この VNet をオンプレミスの場所に接続するには、オンプレミスのネットワーク管理者と調整を行って、この仮想ネットワーク専用に使用できる IP アドレスの範囲を見つけ出す必要があります。 VPN 接続の両側に重複するアドレス範囲が存在する場合、トラフィックが期待どおりにルーティングされない可能性があります。 また、この VNet を別の VNet に接続する場合、アドレス空間を他の VNet と重複させることはできません。 したがって、慎重にネットワーク構成を計画してください。
>
>

1. ブラウザーから [Azure ポータル](http://portal.azure.com) に移動し、Azure アカウントでサインインします。
2. **[リソースの作成]** をクリックします。 **[Marketplace を検索]** フィールドに「仮想ネットワーク」と入力します。 検索結果の一覧から **[仮想ネットワーク]** を探してクリックし、 **[仮想ネットワーク]** ページを開きます。
3. [仮想ネットワーク] ページの下の方にある **[デプロイ モデルの選択]** の一覧で、 **[リソース マネージャー]** を選択し、 **[作成]** をクリックします。 [仮想ネットワークの作成] ページが開きます。

   ![[仮想ネットワークの作成] ページ](./media/vpn-gateway-create-virtual-network-portal-include/create-virtual-network.png "[仮想ネットワークの作成] ページ")
4. **[仮想ネットワークの作成]** ページで、VNet の設定を構成します。 フィールドへの入力時、入力された文字が有効であれば、赤色の感嘆符が緑色のチェック マークに変わります。

   - **[名前]** :仮想ネットワークの名前を入力します。 この例では、VNet1 を使用します。
   - **[アドレス空間]** : アドレス空間を入力します。 追加するアドレス空間が複数ある場合は、1 つ目のアドレス空間を追加してください。 その他のアドレス空間は後で、VNet を作成した後に追加できます。 指定したアドレス空間が、オンプレミスのアドレス空間と重複しないようにしてください。
   - **サブスクリプション**:一覧表示されているサブスクリプションが正しいことを確認します。 ドロップダウンを使用して、サブスクリプションを変更できます。
   - **[リソース グループ]** :既存のリソース グループを選択するか、新しいリソース グループの名前を入力して新しく作成します。 新しいグループを作成する場合は、計画した構成値に基づいて、リソース グループに名前を付けます。 リソース グループの詳細については、「 [Azure リソース マネージャーの概要](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)」を参照してください。
   - **[場所]** :VNet の場所を選択します。 この場所の設定によって、この VNet にデプロイしたリソースの配置先が決まります。
   - **サブネット**:最初のサブネットの名前とアドレス範囲を追加します。 この VNet を作成した後、サブネットとゲートウェイ サブネットを追加できます。 

5. ダッシュボードで VNet を簡単に検索できるようにするには、 **[ダッシュボードにピン留めする]** を選択します。その後、 **[作成]** をクリックします。 **[作成]** をクリックした後で、VNet の進捗状況を反映するタイルがダッシュボードに表示されます。 タイルは、VNet の作成が進むに従って変化します。
