---
title: 証明書の管理 (SQL Server 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b98f52d7c8e23530c13da6ad44d90090998ac09e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68212742"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>証明書の管理 (SQL Server 構成マネージャー)

このトピックでは、SQL Server Always On フェールオーバー クラスターまたは可用性グループ トポロジにわたって証明書を展開および管理する方法について説明します。

SSL/TLS 証明書は、SQL Server へのアクセスをセキュリティで保護するために広く使われています。 以前のバージョンの SQL Server では、大規模な SQL Server の資産を持つ組織は、その SQL Server 証明書インフラストラクチャを維持するために、多くの場合スクリプトを開発したりコマンドを手動で実行したりして、かなりの労力を費やす必要がありました。 SQL Server 2019 では、証明書の管理が SQL Server 構成マネージャーに統合されており、次のような一般的なタスクが簡単になりました。 

* SQL Server インスタンスにインストールされている証明書の表示と検証。 
* 期限切れに近づいている可能性のある証明書の特定。 
* 可用性グループ コンピューターへの証明書の展開 (プライマリ レプリカを保持するノードから)。 
* フェールオーバー クラスター インスタンスに参加しているコンピューターへの証明書の展開 (アクティブなノードから)。

> [!NOTE]
> SQL Server 構成マネージャーの証明書の管理は、SQL Server 2008 以降の古いバージョンの SQL Server で使用できます。

##  <a name="provision-single-server-cert"></a> 1 つの SQL Server インスタンス用の証明書をインストールするには  
  
1. SQL Server 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]** を展開します。  
  
2. **[** *&lt;インスタンス名&gt;* のプロトコル]を右クリックし、 **[プロパティ]** を選択します。  
  
3. **[証明書]** タブを選択し、 **[インポート]** を選択します。  
  
4. **[参照]** を選択し、証明書ファイルを選択します。  
  
5. **[次へ]** を選択して、証明書を検証します。 エラーがない場合は、 **[次へ]** を選択して、ローカル インスタンスに証明書をインポートします。  
  
 
##  <a name="provision-failover-cluster-cert"></a> フェールオーバー クラスター構成で証明書をインストールするには  
  
1. SQL Server 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]** を展開します。
  
2. **[** *&lt;インスタンス名&gt;* のプロトコル]を右クリックし、 **[プロパティ]** を選択します。 

3. **[証明書]** タブを選択し、 **[インポート]** を選択します。

4. 証明書の種類を選択し、現在のノードに対してのみインポートするか、または個々のクラスター ノードごとにインポートするかを選択します。

5. 1 つのノードに対してインストールする場合は、 **[参照]** を選択し、証明書ファイルを選択します。 その後、手順 8. に進みます。

6. ノードごとに証明書をインストールする場合は、 **[次へ]** を選択して、所有者ノード候補を一覧表示します。 現在の SQL Server FCI の所有者候補が、あらかじめ選択されています。

7. **[次へ]** を選択して、インポートする証明書を選択します。

8. パスワードの入力を求められたら、入力します。 検証後に、警告やエラーを探します。

9. **[次へ]** を選択して、選択した証明書をインポートします。

> [!NOTE]
> これらの手順は、SQL Server フェールオーバー クラスター インスタンスのアクティブ ノードで実行します。 ユーザーには、すべてのクラスター ノードでの管理者権限が必要です。

##  <a name="provision-availability-group-cert"></a>可用性グループ構成で証明書をインストールするには  
  
1. SQL Server 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]** を展開します。
  
2. **[** *&lt;インスタンス名&gt;* のプロトコル]を右クリックし、 **[プロパティ]** を選択します。  
  
3. **[証明書]** タブを選択し、 **[インポート]** を選択します。  
  
4. 証明書の種類を選択し、 **[次へ]** を選択して、既知の可用性グループの一覧から選択します。  

5. **[次へ]** を選択して、各レプリカ ノード用の証明書を選択します。 証明書のファイル名は、ノードの NetBios 名と一致する必要があります。

6. **[次へ]** を選択して、各ノードに選択した証明書をインポートします。


> [!NOTE]
> これらの手順は、可用性グループのプライマリ レプリカを保持しているノードから実行します。 ユーザーには、すべてのクラスター ノードでの管理者権限が必要です。

