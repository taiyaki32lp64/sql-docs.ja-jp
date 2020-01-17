---
title: サーバーのスタートアップ オプションの構成 (SQL Server 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- SQL Server services, setting startup options
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 91a48d4acd771c19617bac26c1393f30334768e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810370"
---
# <a name="configure-server-startup-options-sql-server-configuration-manager"></a>サーバーのスタートアップ オプションの構成 (SQL Server 構成マネージャー)
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、[!INCLUDE[ssDE](../../includes/ssde-md.md)] が起動するたびに使用するスタートアップ オプションを構成する方法について説明します。 スタートアップ オプションの一覧は、「 [データベース エンジン サービスのスタートアップ オプション](database-engine-service-startup-options.md)」を参照してください。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
### <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは、スタートアップ パラメーターをレジストリに書き込みます。 これらのパラメーターは、次回 [!INCLUDE[ssDE](../../includes/ssde-md.md)]を起動したときに有効になります。  
  
 クラスターでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がオンラインの間にアクティブ サーバー上で変更を行う必要があり、その変更は [!INCLUDE[ssDE](../../includes/ssde-md.md)] を再起動すると有効になります。 他のノードでは、次回のフェールオーバー時にスタートアップ オプションのレジストリが更新されます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 サーバーのスタートアップ オプションの構成は、レジストリの関連エントリを変更できるユーザーのみが使用できます。 該当するユーザーは次のとおりです。  
  
-   ローカル管理者グループのメンバー。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって使用されるドメイン アカウント ( [!INCLUDE[ssDE](../../includes/ssde-md.md)] がドメイン アカウントで実行されるように構成されている場合)。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-configure-startup-options"></a>起動オプションを設定するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで、 **[SQL Server のサービス]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではないため、新しいバージョンの Windows では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーはアプリケーションとして表示されません。  
    >   
    >  -   **Windows 10**:  
    >          開くには[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager で、**スタート ページ**、SQLServerManager12.msc を入力 (の[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の場合は、12 をより小さい数値に置き換えます。 SQLServerManager12.msc をクリックすると、Configuration Manager が開きます。 スタート ページやタスク バーに構成マネージャーをピン留めする SQLServerManager12.msc を右クリックし、**ファイルの場所を開く**します。 Windows エクスプ ローラーで SQLServerManager12.msc を右クリックし、をクリックし、**スタートにピン留め**または**タスクバーにピン留め**します。  
    > -   **Windows 8**:  
    >          開くには[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager で、**検索**チャームの**アプリ**、型**SQLServerManager\<バージョン > .msc** など`SQLServerManager12.msc`、キーを押しますと**Enter**します。  
  
2.  右ペインで、**SQL Server (***<instance_name>***)** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[起動時のパラメーター]** タブの **[起動時のパラメーターの指定]** ボックスにパラメーターを入力し、 **[追加]** をクリックします。  
  
     たとえば、シングル ユーザー モードで起動する次のように入力します。`-m`で、**起動時のパラメーターを指定**ボックスをクリック**追加**します。 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシングル ユーザー モードで再起動する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを停止してください。 そうしないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって先に接続が行われ、2 番目のユーザーとして接続できなくなる場合があります。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]を再起動します。  
  
    > [!WARNING]  
    >  起動時のパラメーター ボックスでのシングル ユーザー モードでの使用が終了したら、選択、`-m`パラメーター、**既存のパラメーター**ボックスをクリックして**削除**します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] を再起動すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が通常のマルチユーザー モードに戻ります。  
  
## <a name="see-also"></a>関連項目  
 [シングル ユーザー モードでの SQL Server の起動](start-sql-server-in-single-user-mode.md)   
 [システム管理者がロックアウトされた場合の SQL Server への接続](connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [SQL Server エージェント サービスの開始、停止、または一時停止](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
