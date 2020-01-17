---
title: Controller および Client のサービス アカウントの変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 44a73ddb-18ad-415c-bfbe-126ab2e3290b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9f9439fd1b0844b09e26331859ce37d18817f908
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62505992"
---
# <a name="modify-the-controller-and-client-services-accounts"></a>Controller および Client のサービス アカウントの変更
  このトピックでは、分散再生コントローラーと分散再生クライアントのサービス アカウントを変更し、アクセス制御リスト (ACL) を再度適用する方法について説明します。  
  
### <a name="to-start-or-stop-the-distributed-replay-services-using-computer-management"></a>[コンピューターの管理] を使用して 分散再生サービスを開始または停止するには  
  
1.  分散再生サービスがインストールされているコンピューターで、コマンド プロンプトから、「`dcomcnfg`」と入力します。  
  
2.  **[サービス]** をダブルクリックし、下へスクロールして、**[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生 \<サービス名>]** を右クリックします。次に、**[開始]** または **[停止]** をクリックします。  
  
### <a name="to-modify-the-distributed-replay-controller-service"></a>分散再生コントローラー サービスを変更するには  
  
1.  コントローラー コンピューターで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生コントローラー サービスを停止します。  
  
2.  **[サービス]** で、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生コントローラー]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生コントローラーのプロパティ]** ウィンドウの **[ログオン]** タブで、 **[このアカウント]** を選択して、新しいログオン アカウントを入力するか、 **[参照]** をクリックして新しいログオン アカウントを指定し、 **[OK]** をクリックします。  
  
     **重要な**:分散再生コント ローラーを構成するときに、分散再生クライアント サービスの実行に使用される 1 つまたは複数のユーザー アカウントを指定できます。 サポートされているアカウントの一覧を次に示します。  
  
    -   ドメイン ユーザー アカウント  
  
    -   ユーザーによって作成されたローカル ユーザー アカウント  
  
    -   管理者  
  
    -   仮想アカウントおよび管理されたサービス アカウント (MSA)  
  
    -   ネットワーク サービス、ローカル サービス、およびシステム  
  
     グループ アカウント (ローカルまたはドメイン) およびその他の組み込みのアカウント (Everyone など) は使用できません。  
  
4.  分散再生コントローラー サービスを開始します。  
  
### <a name="to-modify-the-distributed-replay-client-service"></a>分散再生クライアント サービスを変更するには  
  
1.  分散再生クライアント サービスを変更する前に、変更する分散再生クライアントのサービス アカウントが、セットアップ時にコントローラー コンピューターの CTLRUSERS パラメーターに指定されていることを確認してください。 変更する分散再生クライアントのサービス アカウントがセットアップ時に指定されていない場合は、先に次の手順を実行する必要があります。  
  
    1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生コントローラー サービスを停止します。  
  
    2.  分散再生コントローラー サービスがインストールされているコントローラー コンピューターで、コマンド プロンプトから、「`dcomcnfg`」と入力します。  
  
    3.  **[コンポーネント サービス]** ウィンドウで、**[コンソール ルート]、[コンポーネント サービス]、[コンピューター]、[マイ コンピューター]、[DCOM 構成]、[DReplayController]** に移動します。  
  
    4.  **[DReplayController]** を右クリックし、**[プロパティ]** をクリックします。  
  
    5.  **[DReplayController のプロパティ]** ウィンドウの **[セキュリティ]** タブで、 **[起動とアクティブ化のアクセス許可]** セクションの **[編集]** をクリックします。  
  
    6.  新しいクライアント サービス ログオン アカウントに **ローカルとリモートからのアクティブ化** 権限を与え、 **[OK]** をクリックします。  
  
    7.  **[アクセス許可]** セクションの **[編集]** をクリックし、新しいクライアント サービス ログオン アカウントに **ローカルとリモートのアクセス権限** を与え、 **[OK]** をクリックします。  
  
    8.  **[OK]** をクリックして、 **[DReplayController のプロパティ]** ウィンドウを閉じます。  
  
    9. コントローラー コンピューターで、変更したクライアント サービス ログオン アカウントを **Distributed COM Users** グループに追加します。  
  
    10. SQL Server 分散再生コントローラー サービスを開始します。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生クライアント サービスを停止します。  
  
3.  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生クライアントのプロパティ]** ウィンドウの **[ログオン]** タブで、 **[このアカウント]** を選択して、新しいログオン アカウントを入力するか、 **[参照]** をクリックして新しいログオン アカウントを指定し、 **[OK]** をクリックします。  
  
4.  分散再生クライアント サービスを開始します。  
  
  
