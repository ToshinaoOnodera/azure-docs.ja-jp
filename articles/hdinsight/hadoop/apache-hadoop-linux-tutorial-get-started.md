---
title: クイック スタート:Resource Manager を使用して Apache Hadoop クラスターを作成する - Azure HDInsight
description: HDInsight クラスターを作成する方法について説明します。
keywords: Hadoop の概要, Hadoop Linux, Hadoop クイックスタート, Hive の概要, Hive クイックスタート
ms.service: hdinsight
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.custom: hdinsightactive,hdiseo17may2017,mvc,seodec18
ms.topic: quickstart
ms.date: 05/14/2019
ms.openlocfilehash: 9084e8e0fe7707b5f115df80792cea102772b8e9
ms.sourcegitcommit: 4c2b9bc9cc704652cc77f33a870c4ec2d0579451
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65861642"
---
# <a name="quickstart-create-apache-hadoop-cluster-in-azure-hdinsight-using-resource-manager-template"></a>クイック スタート:Resource Manager テンプレートを使用して Azure HDInsight で Apache Hadoop クラスターを作成する

このクイック スタートでは、Resource Manager テンプレートを使用して Azure HDInsight で Apache Hadoop クラスターを作成する方法を学習します。

同じようなテンプレートを「[Azure クイック スタート テンプレート](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Hdinsight&pageNumber=1&sort=Popular)」で見ることができます。 テンプレートのリファレンスについては、[こちら](https://docs.microsoft.com/azure/templates/microsoft.hdinsight/allversions)をご覧ください。  また、[Azure portal](apache-hadoop-linux-create-cluster-get-started-portal.md) を使用してクラスターを作成することもできます。  

現在、HDInsight には [7 種類のクラスター](./apache-hadoop-introduction.md#cluster-types-in-hdinsight)が用意されています。 クラスターの種類はそれぞれ異なるコンポーネント セットをサポートしていますが、 Hive は全種類のクラスターでサポートされています。 HDInsight でサポートされているコンポーネントの一覧については、「[HDInsight で提供される Hadoop クラスター バージョンの新機能](../hdinsight-component-versioning.md)」を参照してください。  

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウントを作成](https://azure.microsoft.com/free/)してください。

<a name="create-cluster"></a>
## <a name="create-a-hadoop-cluster"></a>Hadoop クラスターの作成

1. 下の **[Azure へのデプロイ]** ボタンを選択して Azure にサインインし、Azure portal で Resource Manager テンプレートを開きます。
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/apache-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. 次の値を入力または選択します。

    |プロパティ  |説明  |
    |---------|---------|
    |**サブスクリプション**     |  Azure サブスクリプションを選択します。 |
    |**リソース グループ**     | リソース グループを作成するか、既存のリソース グループを選択します。  リソース グループとは、Azure コンポーネントのコンテナーです。  この場合、リソース グループには、HDInsight クラスターおよび依存する Azure ストレージ アカウントが含まれています。 |
    |**場所**     | クラスターを作成する Azure の場所を選択します。  パフォーマンスを向上させるため、お近くの場所を選択してください。 |
    |**クラスター名**     | Hadoop クラスターの名前を入力します。 HDInsight のすべてのクラスターでは同じ DNS 名前空間が共有されるため、この名前は一意である必要があります。 名前に使用できるのは小文字、数字、ハイフンのみであり、名前の先頭は文字にする必要があります。  各ハイフンの前後にはハイフン以外の文字を指定する必要があります。  また、名前は 3 から 59 文字の範囲でなければなりません。 |
    |**クラスターの種類**     | **[hadoop]** を選択します。 |
    |**クラスター ログイン名とパスワード**     | 既定のログイン名は **admin** です。パスワードは 10 文字以上で、数字、大文字、小文字、英数字以外の文字 (' " ` を除く\) が少なくとも 1 つずつ含まれる必要があります。 "Pass@word1" などのよく使われるパスワードを**指定していない**ことを確認してください。|
    |**SSH ユーザー名とパスワード**     | 既定のユーザー名は **sshuser** です。  SSH ユーザー名は、変更が可能です。  SSH ユーザーのパスワードには、クラスターのログイン パスワードと同じ要件が適用されます。|

    一部のプロパティは、テンプレートにハードコーディングされています。  これらの値はテンプレートから構成することができます。 これらのプロパティについて詳しくは、[HDInsight での Apache Hadoop クラスターの作成](../hdinsight-hadoop-provision-linux-clusters.md)に関するページをご覧ください。

    > [!NOTE]  
    > 指定する値は一意である必要があり、名前付けガイドラインに従う必要があります。 テンプレートでは、検証チェックは実行されません。 指定した値が既に使用されている場合、またはガイドラインに従ってない場合、テンプレートを送信した後にエラーが発生します。  

    ![HDInsight Linux の使用。ポータルの Resource Manager テンプレート](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "Azure portal とリソース グループ マネージャー テンプレートを使用して HDInsight で Hadoop クラスターをデプロイする")

3. **[上記の使用条件に同意する]** を選択し、 **[購入]** を選択します。 デプロイの進行状況が通知されます。  クラスターの作成には約 20 分かかります。

4. クラスターが作成されると、 **[リソース グループに移動]** リンクを含む**デプロイ成功**通知を受け取ります。  **[リソース グループ]** ページには、新しい HDInsight クラスターと、クラスターに関連付けられている既定のストレージが一覧表示されます。 各クラスターには、[Azure Storage アカウント](../hdinsight-hadoop-use-blob-storage.md)または [Azure Data Lake Storage アカウント](../hdinsight-hadoop-use-data-lake-store.md)との依存関係があります。 このアカウントを、既定のストレージ アカウントと呼びます。 HDInsight クラスターとその既定のストレージ アカウントは、同じ Azure リージョンに配置されている必要があります。 クラスターを削除しても、ストレージ アカウントは削除されません。

> [!NOTE]  
> その他のクラスター作成方法や、このクイック スタートで使用されているプロパティについては、[HDInsight クラスターの作成](../hdinsight-hadoop-provision-linux-clusters.md)に関するページを参照してください。

## <a name="troubleshoot"></a>トラブルシューティング

HDInsight クラスターの作成で問題が発生した場合は、「[アクセス制御の要件](../hdinsight-hadoop-customize-cluster-linux.md#access-control)」を参照してください。

## <a name="clean-up-resources"></a>リソースのクリーンアップ
このクイックスタートを完了したら、必要に応じてクラスターを削除できます。 HDInsight を使用すると、データは Azure Storage に格納されるため、クラスターは、使用されていない場合に安全に削除できます。 また、HDInsight クラスターは、使用していない場合でも課金されます。 クラスターの料金は Storage の料金の何倍にもなるため、クラスターを使用しない場合は削除するのが経済的にも合理的です。

> [!NOTE]  
> *すぐに*次のチュートリアルに進み、HDInsight で Hadoop を使用して ETL 操作を実行する方法を学習する場合は、クラスターを実行したままにしておいてかまいません。 これは、そのチュートリアルでは Hadoop クラスターを再度作成する必要があるからです。 ただし、すぐに次のチュートリアルに進まない場合は、クラスターを今すぐ削除する必要があります。

**クラスターと既定のストレージ アカウントを削除するには、次の手順に従います。**

1. ブラウザーの Azure Portal を開いているタブに戻ります。 [クラスターの概要] ページが表示されているはずです。 クラスターのみを削除し、既定のストレージ アカウントを保持する場合は、 **[削除]** を選択します。

    ![HDInsight におけるクラスターの削除](./media/apache-hadoop-linux-tutorial-get-started/hdinsight-delete-cluster.png "HDInsight クラスターの削除")

2. クラスターと既定のストレージ アカウントを削除する場合は、(上のスクリーンショットで強調表示されている) リソース グループ名を選択して、リソース グループのページを開きます。

3. **[リソース グループの削除]** を選択して、クラスターと既定のストレージ アカウントが含まれたリソース グループを削除します。 リソース グループを削除するとストレージ アカウントも削除されます。 ストレージ アカウントを残しておく場合は、クラスターのみを削除してください。

## <a name="next-steps"></a>次の手順

このクイック スタートでは、Resource Manager テンプレートを使用して HDInsight で Apache Hadoop クラスターを作成する方法を学習しました。 次の記事では、HDInsight で Hadoop を使用して抽出、変換、読み込み (ETL) 操作を実行する方法を学習します。

> [!div class="nextstepaction"]
>[HDInsight での Apache Hive を使用したデータの抽出、変換、読み込み](../hdinsight-analyze-flight-delay-data-linux.md)

実際のデータを使用する準備が整っていて、HDInsight のデータの格納方法や HDInsight にデータを取り込む方法を確認する場合は、以下の記事を参照してください。

* HDInsight で Azure Storage を使用する方法の詳細については、[HDInsight での Azure Storage の使用](../hdinsight-hadoop-use-blob-storage.md)に関するページを参照してください。
* Data Lake Storage で HDInsight クラスターを作成する方法については、「[Quickstart:Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md)」(クイック スタート: HDInsight のクラスターを設定する) を参照してください。
* データを HDInsight にアップロードする方法については、[データを HDInsight にアップロードする方法](../hdinsight-upload-data.md)に関する記事を参照してください。
* [Azure HDInsight クラスターで Azure Data Lake Storage Gen2 を使用する](../hdinsight-hadoop-use-data-lake-storage-gen2.md)

HDInsight でデータを分析する方法の詳細については、次の記事を参照してください。

* Visual Studio から Hive クエリを実行する方法など、HDInsight で Hive を使用する方法の詳細については、[HDInsight での Apache Hive の使用](hdinsight-use-hive.md)に関する記事を参照してください。
* データの変換に使用される言語 Pig の詳細については、[HDInsight での Apache Pig の使用](hdinsight-use-pig.md)に関する記事を参照してください。
* Hadoop 上のデータを処理するプログラムを作成する方法の 1 つである MapReduce の詳細については、[HDInsight での MapReduce の使用](hdinsight-use-mapreduce.md)に関する記事を参照してください。
* HDInsight Tools for Visual Studio を使用して HDInsight 上のデータを分析する方法については、 [HDInsight Hadoop Tools for Visual Studio の使用開始](apache-hadoop-visual-studio-tools-get-started.md)に関するページを参照してください。
* HDInsight Tools for VS Code を使用して HDInsight 上のデータを分析する方法については、「[Azure HDInsight Tool for Visual Studio Code の使用](../hdinsight-for-vscode.md)」をご覧ください。


HDInsight クラスターの作成または管理の詳細については、以下の記事を参照してください。

* Linux ベースの HDInsight クラスターを管理する方法については、[Apache Ambari を使用した HDInsight クラスターの管理](../hdinsight-hadoop-manage-ambari.md)に関するページを参照してください。
* HDInsight クラスターの作成時に選択できるオプションの詳細については、「 [HDInsight での Linux ベースの Hadoop クラスターの作成](../hdinsight-hadoop-provision-linux-clusters.md)」を参照してください。

Azure Resource Manager テンプレートを使用した HDInsight クラスターの作成について詳しくは、以下をご覧ください。

* [Azure クイック スタート テンプレート](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Hdinsight&pageNumber=1&sort=Popular)。
* [Azure テンプレート リファレンス](https://docs.microsoft.com/azure/templates/microsoft.hdinsight/allversions)。

[1]: ../HDInsight/apache-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md