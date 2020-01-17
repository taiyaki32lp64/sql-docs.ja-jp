---
title: Azure のレプリカ追加ウィザードの使用 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90418193ac869641a20f8b0f684fc43dd46712f8
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175994"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Azure のレプリカ追加ウィザードの使用 (SQL Server)
  Azure のレプリカ追加ウィザードを使用して、ハイブリッド IT で新しい Azure VM を作成し、新規または既存の AlwaysOn 可用性グループのセカンダリレプリカとして構成することができます。  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
     [セキュリティ](#Security)  
  
-   **レプリカを追加する方法:**  [Azure のレプリカ追加ウィザード (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 可用性グループに可用性レプリカを追加したことがない場合は、「サーバーインスタンス」と「可用性グループとレプリカ」のセクション「 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の前提条件、制限事項、推奨事項](prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
###  <a name="Prerequisites"></a> の前提条件  
  
-   現在のプライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
-   オンプレミスのサブネットに Azure とのサイト間 VPN があるハイブリッド IT 環境が必要です。 詳細については、「 [管理ポータルでのサイト間 VPN の構成](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create)」を参照してください。  
  
-   可用性グループに、内部設置型可用性レプリカが含まれている必要があります。  
  
-   可用性グループ リスナーに対するクライアントで、可用性グループが Azure レプリカにフェールオーバーした場合にリスナーとの接続を維持するには、インターネット接続が必要です。  
  
-   **初期データの完全同期を使用するための前提条件** ウィザードでのバックアップの作成およびバックアップへのアクセスには、ネットワーク共有を指定する必要があります。 プライマリ レプリカでは、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の起動に使用するアカウントにネットワーク共有での読み取り/書き込みファイルシステム権限が必要です。 セカンダリ レプリカでは、アカウントは、ネットワーク共有に対する読み取り権限を持つ必要があります。  
  
     ウィザードを使用して初期データの完全同期を実行できない場合は、セカンダリ データベースを手動で準備する必要があります。 これは、ウィザードの実行前でも実行後でもかまいません。 詳細については、「[可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 「 [Security](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)」を参照してください。  
  
##  <a name="SSMSProcedure"></a> Azure のレプリカ追加ウィザードの使用 (SQL Server Management Studio)  
 Azure のレプリカ追加ウィザードは、 [[レプリカの指定] ページ](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)から起動できます。 このページを開くには、次の 2 つの方法があります。  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Azure のレプリカ追加ウィザードを起動したら、次の手順を行います。  
  
1.  まず、Azure サブスクリプションの管理証明書をダウンロードします。 **[ダウンロード]** をクリックして、サインイン ページを開きます。  
  
2.  サインインページで、Azure サブスクリプションにサインインします。 サインインすると、ローカル コンピューターに管理証明書がインストールされます。 ウィザードを再度使用する場合は、この管理証明書が自動的に読み込まれます。 複数の管理証明書をダウンロードした場合は、 **[...]** ボタンをクリックして、使用する管理証明書を選択します。  
  
3.  次に、 **[接続]** をクリックしてサブスクリプションに接続します。 接続すると、 **[仮想ネットワーク]** や **[仮想ネットワーク サブネット]** などの Azure のパラメーターがドロップダウン リストに設定されます。  
  
4.  新しいセカンダリ レプリカをホストする Azure VM の設定を指定します。  
  
     image  
     Azure VM に使用する SQL Server イメージの名前  
  
     [VM サイズ]  
     Azure VM のサイズ  
  
     [VM 名]  
     Azure VM の DNS 名  
  
     [VM ユーザー名]  
     Azure VM の既定の管理者のユーザー名  
  
     [VM 管理者パスワード] (および [パスワードの確認入力])  
     Azure VM の既定の管理者のパスワード  
  
     [仮想ネットワーク]  
     Azure VM を配置する仮想ネットワーク  
  
     [仮想ネットワーク サブネット]  
     Azure VM を配置する仮想ネットワーク サブネット  
  
     [ドメイン]  
     Azure VM を参加させる Active Directory (AD) ドメイン  
  
     [ドメイン ユーザー名]  
     Azure VM をドメインに参加させるために使用される AD ユーザー名  
  
     Password  
     Azure VM をドメインに参加させるために使用されるパスワード  
  
5.  **[OK]** をクリックして設定をコミットし、Azure のレプリカ追加ウィザードを終了します。  
  
6.  新しいレプリカの場合と同じように、 [[レプリカの指定] ページ](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) で残りの構成手順を行います。  
  
     可用性グループウィザードまたは可用性グループへのレプリカ追加ウィザードでの操作が完了すると、構成プロセスは Azure 内のすべての操作を実行して新しい VM を作成し、それを AD ドメインに参加させ、それを Windows クラスターに追加し、AlwaysOn High を有効にします。可用性グループに新しいレプリカを追加します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の前提条件、制限事項、推奨事項](prereqs-restrictions-recommendations-always-on-availability.md)   
 [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
