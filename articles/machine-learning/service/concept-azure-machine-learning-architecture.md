---
title: アーキテクチャと主要な概念
titleSuffix: Azure Machine Learning service
description: Azure Machine Learning service を構成するアーキテクチャ、用語、概念、およびワークフローについて説明します。
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual
ms.author: larryfr
author: Blackmist
ms.date: 04/15/2019
ms.custom: seodec18
ms.openlocfilehash: 8bb06d04aec8e98308c0f5595b6b39e4b98302ff
ms.sourcegitcommit: cababb51721f6ab6b61dda6d18345514f074fb2e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66480062"
---
# <a name="how-azure-machine-learning-service-works-architecture-and-concepts"></a>Azure Machine Learning service のしくみ:アーキテクチャと概念

Azure Machine Learning service のアーキテクチャ、概念、ワークフローについて説明します。 サービスの主要なコンポーネントと、サービスを使用する場合の一般的なワークフローを、以下の図に示します。

[![Azure Machine Learning service のアーキテクチャとワークフロー](./media/concept-azure-machine-learning-architecture/workflow.png)](./media/concept-azure-machine-learning-architecture/workflow.png#lightbox)

## <a name="workflow"></a>ワークフロー

機械学習のワークフローの一般的なシーケンスは次のとおりです。

1. **Python** で機械学習トレーニング スクリプトを開発します。
1. **コンピューティング ターゲット** を作成して構成します。
1. 構成したコンピューティング ターゲットに **スクリプトを送信** して、その環境で実行します。 トレーニング中、このスクリプトは、**データストア**の読み取りと書き込みを行うことができます。 そして実行の記録は、**ワークスペース**に**実行**として保存され、**実験**の下でグループ化されます。
1. 現在と過去の実行から **実験をクエリ** してログに記録されたメトリックを取得します。 メトリックで目的の結果が示されない場合は、手順 1 に戻ってスクリプトを繰り返します。
1. 満足できる実行が見つかった場合は、永続化されたモデルを**モデル レジストリ**に登録します。
1. モデルを使用するスコアリング スクリプトを開発し、**Web サービス**として Azure に、または **IoT Edge デバイス**に**モデルをデプロイ**します。

次のいずれかを使用して、これらの手順を実行できます。
+ [Azure Machine Learning SDK for Python](https://docs.microsoft.com/python/api/overview/azure/ml/intro?view=azure-ml-py)
+ [Azure Machine Learning CLI](https://docs.microsoft.com/azure/machine-learning/service/reference-azure-machine-learning-cli)
+ [Azure Machine Learning VS Code 拡張機能](how-to-vscode-tools.md)
+  [Azure Machine Learning service 用のビジュアル インターフェイス (プレビュー)](ui-concept-visual-interface.md)

> [!NOTE]
> この記事では、Azure Machine Learning service で使用される用語と概念を定義しますが、Azure プラットフォームに関する用語と概念は定義しません。 Azure プラットフォームの用語について詳しくは、[Microsoft Azure 用語集](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology)に関するページを参照してください。

## <a name="workspace"></a>ワークスペース

[ワークスペース](concept-workspace.md)は、Azure Machine Learning service の最上位のリソースです。 Azure Machine Learning service を使用するときに作成する、すべての成果物を操作するための一元的な場所が提供されます。

ワークスペースの分類を次の図に示します。

[![ワークスペースの分類](./media/concept-azure-machine-learning-architecture/azure-machine-learning-taxonomy.png)](./media/concept-azure-machine-learning-architecture/azure-machine-learning-taxonomy.png#lightbox)

ワークスペースの詳細については、「[Azure Machine Learning ワークスペースの管理](concept-workspace.md)」をご覧ください。

## <a name="experiment"></a>実験

実験は、指定されたスクリプトからの多くの実行のグループです。 実験は、常に 1 つのワークスペースに属します。 実行を送信するときは、実験名を指定します。 実行に関する情報は、その実験に格納されます。 実行を送信するときに、存在しない実験名を指定すると、新たに指定された名前を持つ新しい実験が自動的に作成されます。

実験の使用例については、[クイック スタート:Azure Machine Learning service の利用の開始](quickstart-run-cloud-notebook.md)に関するページを参照してください。

## <a name="model"></a>モデル

簡単に言うと、モデルとは入力を受け取って出力を生成するひとまとまりのコードです。 機械学習モデルの作成には、アルゴリズムの選択、アルゴリズムへのデータの提供、およびハイパーパラメーターのチューニングが含まれます。 トレーニングはトレーニング済みモデルを生成する反復的なプロセスであり、トレーニング プロセス中にモデルが学習した内容がカプセル化されています。

モデルは、Azure Machine Learning での実行によって生成されます。 Azure Machine Learning の外部でトレーニングされるモデルを使用することもできます。 Azure Machine Learning service ワークスペースにモデルを登録することができます。

Azure Machine Learning service はフレームワークに依存しません。 モデルを作成するときは、Scikit-learn、XGBoost、PyTorch、TensorFlow、Chainer などの任意の人気のある機械学習フレームワークを使用できます。

モデルのトレーニング例については、[チュートリアル: Azure Machine Learning service で画像分類モデルをトレーニングする](tutorial-train-models-with-aml.md)。

### <a name="model-registry"></a>モデル レジストリ

モデル レジストリにより、Azure Machine Learning Services ワークスペース内のすべてのモデルが追跡されます。

モデルは、名前とバージョンによって識別されます。 既存のモデルと同じ名前でモデルを登録するたびに、レジストリではそれが新しいバージョンと見なされます。 バージョンはインクリメントされ、新しいモデルは同じ名前で登録されます。

モデルを登録するときに、追加のメタデータ タグを指定し、モデルを検索するときにそのタグを使用することができます。

アクティブなデプロイで使用されているモデルを削除することはできません。

モデルの登録例については、[Azure Machine Learning での画像分類モデルのトレーニング](tutorial-train-models-with-aml.md)に関するページを参照してください。

## <a name="run-configuration"></a>実行構成

実行構成は、指定されたコンピューティング先でのスクリプトの実行方法を定義する一連の命令です。 構成には、既存の Python 環境を使用するかどうかや、仕様から構築される Conda 環境を使用するかどうかなど、広範な動作の定義セットが含まれます。

実行構成は、トレーニング スクリプトが含まれるディレクトリ内のファイルに保持することも、メモリ内オブジェクトとして構築して実行の送信に使用することもできます。

実行構成の例については、[モデルをトレーニングするためのコンピューティング先の選択と使用](how-to-set-up-training-targets.md)に関するページを参照してください。

## <a name="dataset"></a>Dataset

Azure Machine Learning Datasets (プレビュー) は、データへのアクセスと操作を容易にします。 データセットは、モデルのトレーニングやパイプラインの作成など、さまざまなシナリオでデータを管理します。 Azure Machine Learning SDK を使用すると、基礎となるストレージへのアクセス、データの探索と準備、異なるデータセット定義のライフ サイクルの管理、トレーニングと運用環境で使用されるデータセット間の比較が可能になります。

Datasets には、`from_delimited_files()` や `to_pandas_dataframe()` を使用するなど、一般的なフォーマットでデータを操作する方法が用意されています。

詳細については、[Azure Machine Learning Datasets の作成と登録](how-to-create-register-datasets.md)に関するページを参照してください。

Datasets の使用例については、[サンプル ノートブック](https://aka.ms/dataset-tutorial)を参照してください。

## <a name="datastore"></a>データストア

データストアは、Azure ストレージ アカウントに対するストレージの抽象化です。 データストアでは、バックエンド ストレージとして Azure BLOB コンテナーまたは Azure ファイル共有を使用できます。 各ワークスペースには既定のデータストアがあり、ユーザーは追加のデータストアを登録できます。

データストアのファイルを格納および取得するには、Python SDK API または Azure Machine Learning CLI を使用します。

## <a name="compute-target"></a>コンピューティング ターゲット

コンピューティング先は、トレーニング スクリプトを実行するために、またはサービスのデプロイをホストするために使用するコンピューティング リソースです。 サポートされているコンピューティング ターゲットを次に示します。

| コンピューティング ターゲット | トレーニング | Deployment |
| ---- |:----:|:----:|
| ユーザーのローカル コンピューター | ✓ | &nbsp; |
| Azure Machine Learning コンピューティング | ✓ | &nbsp; |
| Azure の Linux VM</br>(Data Science Virtual Machine など) | ✓ | &nbsp; |
| Azure Databricks | ✓ | &nbsp; |
| Azure Data Lake Analytics | ✓ | &nbsp; |
| Apache Spark for HDInsight | ✓ | &nbsp; |
| Azure Container Instances | &nbsp; | ✓ |
| Azure Kubernetes Service | &nbsp; | ✓ |
| Azure IoT Edge | &nbsp; | ✓ |
| フィールド プログラマブル ゲート アレイ (FPGA) | &nbsp; | ✓ |

コンピューティング ターゲットはワークスペースに接続されています。 ローカル コンピューター以外のコンピューティング ターゲットは、ワークスペースのユーザーによって共有されます。

### <a name="managed-and-unmanaged-compute-targets"></a>マネージドおよびアンマネージド コンピューティング先

* **マネージド**:Azure Machine Learning service によって作成および管理されるコンピューティング先。 これらのコンピューティング先は、機械学習ワークロード向けに最適化されています。 2018 年 12 月 4 日の時点では、Azure Machine Learning コンピューティングが唯一のマネージド コンピューティング先となります。 今後、他のマネージド コンピューティング先が追加される予定です。

    機械学習コンピューティング インスタンスは、Azure ポータル、Azure Machine Learning SDK、または Azure CLI を使用して、ワークスペースから直接作成できます。 他のコンピューティング先はすべて、ワークスペースの外部で作成してから、そのワークスペースに接続する必要があります。

* **アンマネージド**:Azure Machine Learning service によって管理され*ない* コンピューティング先。 Azure Machine Learning の外部で作成してから、使用する前にご利用のワークスペースに接続する必要がある場合があります。 アンマネージド コンピューティング先では、機械学習ワークロードのパフォーマンスを維持するため、または向上させるために追加の手順が必要になる場合があります。

トレーニング用のコンピューティング先の選択については、[モデルをトレーニングするためのコンピューティング先の選択と使用](how-to-set-up-training-targets.md)に関するページを参照してください。

デプロイ用のコンピューティング先の選択については、[Azure Machine Learning service でのモデルのデプロイ](how-to-deploy-and-where.md)に関するページを参照してください。

## <a name="training-script"></a>トレーニング スクリプト

モデルをトレーニングするには、トレーニング スクリプトおよび関連ファイルが格納されているディレクトリを指定します。 実験名も指定します。これは、トレーニング中に収集される情報を格納するために使用されます。 トレーニング中に、ディレクトリ全体がトレーニング環境 (コンピューティング先) にコピーされて、実行構成で指定されるスクリプトが開始されます。 ディレクトリのスナップショットも、ワークスペース内の実験の下に格納されます。

例については、「[チュートリアル:Azure Machine Learning service で画像分類モデルをトレーニングする](tutorial-train-models-with-aml.md)。

## <a name="run"></a>ラン

実行は、次の情報を含むレコードです。

* 実行に関するメタデータ (タイムスタンプ、期間など)
* スクリプトによって記録されるメトリック
* 実験によって自動収集される、またはユーザーによって明示的にアップロードされる、出力ファイル
* 実行前の、スクリプトを含むディレクトリのスナップショット

モデルをトレーニングするためにスクリプトを送信するときに実行を生成します。 実行は、0 個以上の子実行を持つことができます。 たとえば、最上位レベルの実行は 2 つの子実行を持つ可能性があり、それぞれが独自の子実行を持つ場合があります。

モデルのトレーニングによって生成される実行を表示する例については、[クイック スタート: Azure Machine Learning service の利用の開始](quickstart-run-cloud-notebook.md)に関するページを参照してください。

## <a name="github-tracking-and-integration"></a>GitHub の追跡と統合

ソース ディレクトリがローカル Git リポジトリであるトレーニング実行を開始すると、リポジトリに関する情報が実行履歴に格納されます。 たとえば、リポジトリの現在のコミット ID が履歴の一部としてログに記録されます。 これは、推定器、ML パイプライン、またはスクリプトの実行を使用して送信した実行で機能します。 SDK または Machine Learning CLI から送信された実行でも機能します。

## <a name="snapshot"></a>スナップショット

実行を送信するときに、Azure Machine Learning によって、スクリプトが含まれているディレクトリが zip ファイルとして圧縮され、コンピューティング先に送られます。 その後、zip ファイルが抽出され、そこでスクリプトが実行されます。 Azure Machine Learning では、zip ファイルもスナップショットとして実行レコード内に格納されます。 ワークスペースにアクセスできるすべてのユーザーは、実行レコードを参照し、スナップショットをダウンできます。

> [!NOTE]
> 不要なファイルがスナップショットに含まれないようにするため、無視ファイル (.gitignore または .amlignore) を作成します。 このファイルをスナップショット ディレクトリに配置し、無視するファイルの名前をその中に追加します。 .amlignore ファイルには、[.gitignore ファイルと同じ構文とパターン](https://git-scm.com/docs/gitignore)が使用されます。 両方のファイルが存在する場合、.amlignore ファイルが優先されます。

## <a name="activity"></a>アクティビティ

アクティビティは、実行時間の長い操作を表します。 次の操作はアクティビティの例です。

* コンピューティング ターゲットの作成または削除
* コンピューティング ターゲット上でのスクリプトの実行

アクティビティでは、ユーザーがこれらの操作の進行状況を簡単に監視できるように、SDK または Web UI 経由で通知を提供できます。

## <a name="image"></a>Image

イメージによって、モデルを使用するために必要なすべてのコンポーネントと共に、モデルを確実にデプロイする方法が提供されます。 イメージには次の項目が含まれます。

* モデル。
* スコアリング スクリプトまたはアプリケーション。 スクリプトを使用して、モデルに入力を渡し、モデルから出力を戻します。
* モデルまたはスコアリング スクリプトあるいはアプリケーションで必要な依存関係。 たとえば、Python パッケージの依存関係が列記されている Conda 環境ファイルを含めることがあります。

Azure Machine Learning では、次の 2 種類のイメージを作成できます。

* **FPGA イメージ**:Azure のフィールド プログラマブル ゲート アレイにデプロイするときに使用されます。
* **Docker イメージ**:FPGA 以外のコンピューティング先にデプロイするときに使用されます。 例として、Azure Container Instances や Azure Kubernetes Service があります。

Azure Machine Learning service は基本イメージを提供し、それが既定で使用されます。 独自のカスタム イメージを指定することもできます。

イメージの作成例については、「[Azure Container Instances に画像分類モデルをデプロイする](tutorial-deploy-models-with-aml.md)」を参照してください。

### <a name="image-registry"></a>イメージ レジストリ

イメージ レジストリでは、モデルから作成されたイメージを追跡します。 イメージを作成するときに、追加のメタデータ タグを指定できます。 メタデータ タグは、イメージ レジストリによって格納され、イメージを検索するためにクエリを実行できます。

## <a name="deployment"></a>Deployment

デプロイは、クラウドでホストできる Web サービスまたは統合デバイスのデプロイ用 IoT モジュールへのモデルのインスタンス化です。

### <a name="web-service"></a>Web サービス

デプロイされた Web サービスでは、Azure Container Instances、Azure Kubernetes Service、または FPGA を使用できます。 モデル、スクリプト、および関連ファイルからサービスを作成します。 これらはイメージにカプセル化されており、Web サービスにランタイム環境を提供します。 イメージには、Web サービスに送信されるスコアリング要求を受け取る、負荷分散された HTTP エンドポイントがあります。

Azure には Application Insights のテレメトリやモデルのテレメトリを収集する機能があり、それを有効にすると、Web サービスのデプロイを監視するのに役立ちます。 利用統計情報にアクセスできるのは機能を有効にしたユーザーだけであり、情報はそのユーザーの Application Insights インスタンスとストレージ アカウント インスタンスに格納されます。

自動スケールを有効にしてある場合は、Azure でデプロイが自動的にスケーリングされます。

Web サービスとしてのモデルのデプロイ例については、[Azure Container Instances での画像分類モデルのデプロイ](tutorial-deploy-models-with-aml.md)に関するページを参照してください。

### <a name="iot-module"></a>IoT モジュール

デプロイされる IoT モジュールは Docker コンテナーであり、モデルとそれに関連付けられているスクリプトまたはアプリケーション、および追加の依存関係が含まれます。 エッジ デバイス上の Azure IoT Edge を使用して、これらのモジュールをデプロイします。

監視を有効にしてある場合、Azure では Azure IoT Edge モジュール内のモデルから利用統計情報を収集します。 利用統計情報にアクセスできるのは機能を有効にしたユーザーだけであり、情報はそのユーザーのストレージ アカウント インスタンスに格納されます。

Azure IoT Edge ではモジュールが実行されるのを保証し、モジュールをホストしているデバイスを監視します。

## <a name="pipeline"></a>パイプライン

機械学習パイプラインを使用し、機械学習フェーズをつなげるワークフローを作成して管理します。 たとえば、パイプラインには、データ準備、モデル トレーニング、モデル デプロイ、推論/スコアリングの各フェーズが含まれることが考えられます。 それぞれのフェーズには、複数のステップを含めることができ、各ステップは、さまざまなコンピューティング先において無人実行することができます。

このサービスを使用した機械学習パイプラインの詳細については、[パイプラインと Azure Machine Learning](concept-ml-pipelines.md) に関するページを参照してください。

## <a name="logging"></a>ログの記録

ソリューションを開発するときは、Python スクリプトで Azure Machine Learning Python SDK を使用して、任意のメトリックを記録します。 実行後にメトリックのクエリを行って、デプロイするモデルが実行によって生成されたかどうかを判断します。

## <a name="next-steps"></a>次の手順

Azure Machine Learning service の利用を開始する場合は、以下を参照してください。

* [Azure Machine Learning service とは](overview-what-is-azure-ml.md)
* [Azure Machine Learning service のワークスペースを作成する](setup-create-workspace.md)
* [チュートリアル:モデルをトレーニングする](tutorial-train-models-with-aml.md)
* [Resource Manager テンプレートでワークスペースを作成する](how-to-create-workspace-template.md)
