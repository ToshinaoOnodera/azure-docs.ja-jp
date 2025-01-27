---
title: Azure Database for MySQL の価格レベル
description: この記事では、Azure Database for MySQL の価格レベルについて説明します。
author: jan-eng
ms.author: janeng
ms.service: mysql
ms.topic: conceptual
ms.date: 02/01/2019
ms.openlocfilehash: 8e3d12db8d2500a2675e451580bee7072d22d41c
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "66225425"
---
# <a name="azure-database-for-mysql-pricing-tiers"></a>Azure Database for MySQL の価格レベル

Azure Database for MySQL サーバーは、次の 3 つの価格レベルのいずれかで作成できます: Basic、汎用、メモリ最適化。 価格レベルは、プロビジョニングできる仮想コアでのコンピューティング量、仮想コアあたりのメモリ、およびデータの格納に使用されるストレージ テクノロジによって区別されています。 リソースはすべて、MySQL サーバー レベルでプロビジョニングされます。 1 つのサーバーには 1 つ以上のデータベースを含めることができます。

|    | **Basic** | **汎用** | **メモリ最適化** |
|:---|:----------|:--------------------|:---------------------|
| コンピューティング世代 | Gen 4、Gen 5 | Gen 4、Gen 5 | Gen 5 |
| 仮想コア | 1、2 | 2、4、8、16、32、64 |2、4、8、16、32 |
| 仮想コアあたりのメモリ | 2 GB | 5 GB | 10 GB |
| ストレージ サイズ | 5 GB ～ 1 TB | 5 GB ～ 4 TB | 5 GB ～ 4 TB |
| ストレージの種類 | Azure Standard Storage | Azure Premium Storage | Azure Premium Storage |
| データベース バックアップのリテンション期間 | 7 ～ 35 日間 | 7 ～ 35 日間 | 7 ～ 35 日間 |

価格レベルを選択する場合は、まず次の表を参考にしてください。

| 価格レベル | 対象のワークロード |
|:-------------|:-----------------|
| Basic | 低負荷なコンピューティングと I/O パフォーマンスを必要とするワークロード。 たとえば、開発やテスト、使用頻度の低い小規模なアプリケーションに使用するサーバーがこれに該当します。 |
| 汎用 | 負荷分散されたコンピューティングとメモリ、およびスケーラブルな I/O スループットを必要とする大部分のビジネス ワークロード。 たとえば、Web アプリやモバイル アプリ、その他のエンタープライズ アプリケーションをホストするためのサーバーが挙げられます。|
| メモリ最適化 | 高速トランザクション処理と高いコンカレンシーを実現するためのインメモリ パフォーマンスを必要とする、高パフォーマンス データベース ワークロード。 たとえば、リアルタイム データと高パフォーマンスなトランザクション アプリや分析アプリを処理するためのサーバーが挙げられます。|

サーバーを作成したら、仮想コア数、ハードウェアの世代、および価格レベル (Basic への変更と Basic からの変更を除く) を数秒で増やしたり減らしたりできます。 また、アプリケーションのダウンタイムなしでストレージ (増量のみ) とバックアップのリテンション期間 (増減) を個別に調整できます。 バックアップ ストレージの種類は、サーバーの作成後に変更することはできません。 詳細については、「[リソースのスケール](#scale-resources)」セクションを参照してください。

## <a name="compute-generations-and-vcores"></a>コンピューティング世代と仮想コア

コンピューティング リソースは仮想コアとして提供されます。仮想コアは、基礎となるハードウェアの論理 CPU を表します。 中国東部 1、中国北部 1、US DoD 中部、US DoD 東部では、Intel E5-2673 v3 (Haswell) 2.4-GHz プロセッサを基盤とする Gen 4 の論理 CPU を利用します。 それ以外のすべてのリージョンでは、Intel E5-2673 v4 (Broadwell) 2.3 GHz プロセッサを基盤とする Gen 5 論理 CPU を利用します。

## <a name="storage"></a>Storage

プロビジョニングするストレージは、使用している Azure Database for MySQL サーバーで使用可能なストレージ容量です。 ストレージは、データベース ファイル、一時ファイル、トランザクション ログ、および MySQL サーバー ログに使用されます。 プロビジョニングするストレージの合計容量によって、ご利用のサーバーで使用できる I/O 容量も決まります。

|    | **Basic** | **汎用** | **メモリ最適化** |
|:---|:----------|:--------------------|:---------------------|
| ストレージの種類 | Azure Standard Storage | Azure Premium Storage | Azure Premium Storage |
| ストレージ サイズ | 5 GB ～ 1 TB | 5 GB ～ 4 TB | 5 GB ～ 4 TB |
| ストレージの増分サイズ | 1 GB | 1 GB | 1 GB |
| IOPS | 変数 |3 IOPS/GB<br/>最小 100 IOPS<br/>最大 6000 IOPS | 3 IOPS/GB<br/>最小 100 IOPS<br/>最大 6000 IOPS |

サーバーの作成中および作成後にさらにストレージ容量を追加でき、システムではワークロードのストレージ使用量に基づいて自動的にストレージを拡張することができます。 Basic レベルでは、IOPS 保証は提供されません。 汎用およびメモリ最適化の価格レベルでは、IOPS は、プロビジョニング済みのストレージ サイズに合わせて 3 対 1 の比率でスケーリングされます。

ご自身の I/O 使用量を監視するには、Azure Portal または Azure CLI コマンドを使用します。 監視すべき関連メトリックは、[容量の上限、ストレージの割合、ストレージの使用量、および IO の割合](concepts-monitoring.md)です。

### <a name="reaching-the-storage-limit"></a>容量の上限に到達

プロビジョニングされたストレージ容量が 100 GB 未満のサーバーでは、ストレージの空き容量が 512 MB 未満またはプロビジョニングされたストレージ サイズの 5% 未満になった場合に、読み取り専用としてマークされます。 プロビジョニングされたストレージが 100 GB を超えるサーバーでは、ストレージの空き容量が 5 GB 未満になった場合にのみ、読み取り専用としてマークされます。

たとえば、110 GB のストレージをプロビジョニングした場合に、実際の使用量が 105 GB を超えると、サーバーは読み取り専用としてマークされます。 または、5 GB のストレージをプロビジョニングした場合、ストレージの空き容量が 512 MB 未満に達すると、サーバーは読み取り専用としてマークされます。

サービスがサーバーを読み取り専用にしようとしている間、すべての新しい書き込みトランザクション要求はブロックされ、既存のアクティブなトランザクションの実行は継続されます。 サーバーが読み取り専用に設定された場合、後続のすべての書き込み操作とトランザクションのコミットは失敗します。 読み取りクエリは、中断せずに作業を続行します。 プロビジョニングされたストレージを増やすと、サーバーはもう一度書き込みトランザクションを受け入れる準備ができます。

ストレージの自動拡張を有効にするか、サーバーのストレージがしきい値に近づいたときに通知するためのアラートを設定しておくことをお勧めします。そうすると、読み取り専用状態に入ることを防止できます。 詳細については、[アラートの設定方法](howto-alert-on-metric.md)に関するドキュメントをご覧ください。

### <a name="storage-auto-grow"></a>ストレージの自動拡張

ストレージの自動拡張が有効になると、ワークロードに影響を及ぼさずに、ストレージが自動的に拡張されます。 プロビジョニングされたストレージが 100 GB 未満のサーバーでは、ストレージの空き容量が 1 GB 以下またはプロビジョニングされたストレージの 10% 以下になると、プロビジョニングされたストレージ サイズが 5 GB 単位ですぐに拡張されます。 プロビジョニングされたストレージが 100 GB を超えるサーバーでは、ストレージの空き容量がプロビジョニングされたストレージ サイズの 5% 未満になると、プロビジョニングされたストレージ サイズが 5 % 単位で拡張されます。 上記に示したストレージ上限が適用されます。

たとえば、1000 GB のストレージをプロビジョニングした場合、実際の使用量が 950 GB を超えると、サーバーのストレージ サイズは 1050 GB まで拡張されます。 または、10 GB のストレージをプロビジョニングした場合、ストレージの空き容量が 1 GB 未満になったときに、ストレージ サイズが 15 GB へ拡張されます。

## <a name="backup"></a>バックアップ

サービスによって、サーバーのバックアップが自動的に取得されます。 バックアップの最小リテンション期間は 7 日です。 最大 35 日のリテンション期間を設定できます。 リテンション期間は、サーバーの有効期間中、任意の時点で調整できます。 ローカル冗長バックアップまたは geo 冗長バックアップのいずれかを選択することができます。 geo 冗長バックアップは、ご利用のサーバーが作成されたリージョンの [geo ペア リージョン](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)内にも保存されます。 この冗長性により、障害発生時に保護が提供されます。 また、geo 冗長バックアップで使用できるサービスが提供されている他の Azure リージョンに、サーバーを復元できるようになります。 サーバーを作成した後に、2 つのバックアップ ストレージ オプションを切り替えることはできません。

## <a name="scale-resources"></a>リソースのスケール

サーバーの作成後に、仮想コア数、ハードウェアの世代、価格レベル (Basic への変更、および Basic からの変更を除く)、ストレージ量、およびバックアップのリテンション期間を個別に変更できます。 バックアップ ストレージの種類は、サーバーの作成後に変更することはできません。 仮想コアの数は増やしたり減らしたりできます。 バックアップのリテンション期間は、7 日から 35 日の間でスケールアップまたはスケールダウンできます。 ストレージ サイズは増やすことのみ可能です。 ポータルまたは Azure CLI を使用して、リソースのスケーリングを実行できます。 Azure CLI を使用したスケーリングの例については、「[Azure CLI での Azure Database for MySQL サーバーの監視とスケーリング](scripts/sample-scale-server.md)」を参照してください。

仮想コア数、ハードウェアの世代、または価格レベルを変更すると、新しいコンピューティング割り当てを使用して元のサーバーのコピーが作成されます。 新しいサーバーが実行されると、接続が新しいサーバーに切り替わります。 システムが新しいサーバーに切り替わるほんの短時間、新しい接続を確立できず、コミットされていないすべてのトランザクションがロールバックされます。 この時間の長さは変動しますが、ほとんどの場合 1 分未満です。

ストレージのスケーリングおよびバックアップのリテンション期間の変更は、本当の意味でのオンライン操作です。 ダウンタイムはなく、アプリケーションには影響しません。 IOPS はプロビジョニングされたストレージのサイズに合わせてスケーリングされるため、サーバーで使用できる IOPS を増やすには、ストレージをスケールアップします。

## <a name="pricing"></a>価格

最新の料金情報については、サービスの[料金ページ](https://azure.microsoft.com/pricing/details/mysql/)を参照してください。 必要な構成のコストについては、[Azure Portal](https://portal.azure.com/#create/Microsoft.MySQLServer) で、選択したオプションに基づいて表示される **[価格レベル]** タブの月額コストを確認します。 Azure サブスクリプションを取得していない場合は、Azure 料金計算ツールを使用して見積もり価格を確認できます。 [Azure 料金計算ツール](https://azure.microsoft.com/pricing/calculator/)の Web サイトで **[項目の追加]** を選択し、 **[データベース]** カテゴリを展開し、 **[Azure Database for MySQL]** を選択してオプションをカスタマイズします。

## <a name="next-steps"></a>次の手順

- [ポータルで MySQL サーバーを作成](howto-create-manage-server-portal.md)する方法を確認します。
- [サービスの制限](concepts-limits.md)について確認します。
- [読み取りレプリカを使用してスケールアウトする](howto-read-replicas-portal.md)方法を確認します。
