---
title: cloud-init を使用して Azure 上の Linux VM のホスト名を設定する | Microsoft Docs
description: Azure CLI による作成時に cloud-init を使用して Linux VM をカスタマイズする方法
services: virtual-machines-linux
documentationcenter: ''
author: rickstercdn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 11/29/2017
ms.author: rclaus
ms.openlocfilehash: da20c4b30e2708bf7754d025cfbd2c269c3b5c7c
ms.sourcegitcommit: 41ca82b5f95d2e07b0c7f9025b912daf0ab21909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "60648943"
---
# <a name="use-cloud-init-to-set-hostname-for-a-linux-vm-in-azure"></a>cloud-init を使用して Azure の Linux VM のホスト名を設定する
この記事では、Azure でのプロビジョニング時に [cloud-init](https://cloudinit.readthedocs.io) を使用して、仮想マシン (VM) または仮想マシン スケール セット (VMSS) で特定のホスト名を構成する方法を示します。 これらの cloud-init スクリプトは、Azure によってリソースがプロビジョニングされた後の最初の起動時に実行されます。 cloud-init が Azure およびサポートされている Linux ディストリビューションでネイティブに動作する方法の詳細については、[cloud-init の概要](using-cloud-init.md)に関するページをご覧ください

## <a name="set-the-hostname-with-cloud-init"></a>cloud-init でホスト名を設定する
既定では、Azure で新しい仮想マシンを作成するときに、ホスト名は VM 名と同じです。  Azure で [az vm create](/cli/azure/vm) を使用して VM を作成するときに cloud-init スクリプトを実行してこの既定のホスト名を変更するには、`--custom-data` スイッチで cloud-init ファイルを指定します。  

実行中のアップグレード プロセスを表示するには、現在のシェルで *cloud_init_hostname.txt* というファイルを作成し、次の構成を貼り付けます。 この例では、ローカル コンピューター上にない Cloud Shell でファイルを作成します。 任意のエディターを使用することができます。 `sensible-editor cloud_init_hostname.txt` を入力し、ファイルを作成して使用可能なエディターの一覧を確認します。 **nano** エディターを使用するには #1 を選びます。 cloud-init ファイル全体 (特に最初の行) が正しくコピーされたことを確認してください。  

```yaml
#cloud-config
hostname: myhostname
```

このイメージをデプロイする前に、[az group create](/cli/azure/group) コマンドを使用してリソース グループを作成する必要があります。 Azure リソース グループとは、Azure リソースのデプロイと管理に使用する論理コンテナーです。 次の例では、*myResourceGroup* という名前のリソース グループを *eastus* に作成します。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

ここで、[az vm create](/cli/azure/vm) で VM を作成し、次のように `--custom-data cloud_init_hostname.txt` で cloud-init ファイルを指定します。

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroup \
  --name centos74 \
  --image OpenLogic:CentOS:7-CI:latest \
  --custom-data cloud_init_hostname.txt \
  --generate-ssh-keys 
```

作成されると、Azure CLI は VM に関する情報を表示します。 `publicIpAddress` を使用して VM に SSH 接続します。 実際のアドレスを次のように入力します。

```bash
ssh <publicIpAddress>
```

VM 名を表示するには、`hostname` コマンドを次のように使用します。

```bash
hostname
```

VM は、次の出力の例で示すように、cloud-init ファイルで設定された値としてホスト名をレポートします。

```bash
myhostname
```

## <a name="next-steps"></a>次の手順
構成変更の cloud-init の他の例については、以下をご覧ください。
 
- [VM に他の Linux ユーザーを追加する](cloudinit-add-user.md)
- [初回起動時にパッケージ マネージャーを実行して既存のパッケージを更新する](cloudinit-update-vm.md)
- [VM のローカル ホスト名を変更する](cloudinit-update-vm-hostname.md) 
- [アプリケーション パッケージのインストール、構成ファイルの更新、キーの挿入](tutorial-automate-vm-deployment.md)
