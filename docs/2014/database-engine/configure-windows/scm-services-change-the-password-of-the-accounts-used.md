---
title: SQL Server (SQL Server 構成マネージャー) で使用されるアカウントのパスワードの変更 |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- expired password [SQL Server], SQL Server Agent
- passwords [SQL Server], SQL Server Agent service
- passwords [SQL Server], changing
- expired password [SQL Server], Database Engine
- passwords [SQL Server], SQL Server service
- Database Engine [SQL Server], passwords
- changing passwords used by SQL Server
- modifying passwords
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 865c23dc88571e0c9ee317eca280286a6c37118f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810437"
---
# <a name="change-the-password-of-the-accounts-used-by-sql-server-sql-server-configuration-manager"></a>SQL Server で使用されるアカウントのパスワードの変更 (SQL Server 構成マネージャー)
  このトピックでは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] で SQL Server 構成マネージャーを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] エージェントによって使用されるアカウントのパスワードを変更する方法について説明します。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、セットアップ時に最初に指定される資格情報を使用して、コンピューター上でサービスとして実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがドメイン アカウントで実行されていて、そのアカウントのパスワードが変更された場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されているパスワードを新しいパスワードに更新する必要があります。 パスワードを更新しないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は一部のドメイン リソースにアクセスできなくなる可能性があります。また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が停止すると、パスワードを更新するまでサービスが再開されません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のパスワードを変更するには、「 [[パスワードの有効期限が切れました]](../password-expired.md)」を参照してください。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの設定を変更するように設計および承認されたツールです。 Windows サービス コントロール マネージャー ( **services.msc** ) アプリケーションを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを変更すると、必要なすべての設定が変更されず、サービスが適切に機能しない場合があります。 ただし、クラスター環境では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用してアクティブ ノードのパスワードを変更した後、サービス コントロール マネージャーを使用してパッシブ ノードでパスワードを変更する必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 サービスで使用されるパスワードを変更するには、コンピューターの管理者である必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-change-the-password-used-by-the-sql-server-database-engine-service"></a>SQL Server (データベース エンジン) サービスで使用されるパスワードを変更するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではないため、新しいバージョンの Windows では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーはアプリケーションとして表示されません。  
    >   
    >  -   **Windows 10**:  
    >          開くには[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager で、**スタート ページ**、SQLServerManager12.msc を入力 (の[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の場合は、12 をより小さい数値に置き換えます。 SQLServerManager12.msc をクリックすると、Configuration Manager が開きます。 スタート ページやタスク バーに構成マネージャーをピン留めする SQLServerManager12.msc を右クリックし、**ファイルの場所を開く**します。 Windows エクスプ ローラーで SQLServerManager12.msc を右クリックし、をクリックし、**スタートにピン留め**または**タスクバーにピン留め**します。  
    > -   **Windows 8**:  
    >          開くには[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager で、**検索**チャームの**アプリ**、型**SQLServerManager\<バージョン > .msc** など`SQLServerManager12.msc`、キーを押しますと**Enter**します。  
  
2.  SQL Server 構成マネージャーで **[SQL Server のサービス]** をクリックします。  
  
3.  詳細ペインで **[SQL Server (** \<instancename> **)]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[SQL Server (** \<instancename> **) のプロパティ]** ダイアログ ボックスの [ログオン] タブで、 **[アカウント名]** ボックスに表示されるアカウントの新しいパスワードを **[パスワード]** ボックスと **[パスワードの確認入力]** ボックスに入力して、 **[OK]** をクリックします。  
  
     パスワードは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動しなくてもすぐに有効になります。  
  
#### <a name="to-change-the-password-used-by-the-sql-server-agent-service"></a>SQL Server エージェント サービスで使用されるパスワードを変更するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  SQL Server 構成マネージャーで **[SQL Server のサービス]** をクリックします。  
  
3.  詳細ペインで **[SQL Server エージェント (** \<instancename> **)]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[SQL Server エージェント (** \<instancename> **) のプロパティ]** ダイアログ ボックスの [ログオン] タブで、 **[アカウント名]** ボックスに表示されるアカウントの新しいパスワードを **[パスワード]** ボックスと **[パスワードの確認入力]** ボックスに入力して、 **[OK]** をクリックします。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のスタンドアロン インスタンスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動しなくてもパスワードがすぐに有効になります。 クラスター インスタンスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースをオフラインにする場合があり、再起動が必要になります。  
  
## <a name="see-also"></a>参照  
 [サービスの管理方法に関するトピック &#40;SQL Server 構成マネージャー&#41;](../managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
  
