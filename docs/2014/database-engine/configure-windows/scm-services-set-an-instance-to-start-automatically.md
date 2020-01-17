---
title: SQL Server のインスタンスを自動的に開始する設定 (SQL Server 構成マネージャー) |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 300b539e132b9bda9bc6540c0aadcac6ab9f11a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810027"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>SQL Server のインスタンスが自動的に開始されるようにする設定 (SQL Server 構成マネージャー)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で SQL Server 構成マネージャーを使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスを自動的に開始するように設定する方法について説明します。 セットアップのとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は通常、自動的に開始するように構成されます。 手動で開始するように構成した場合、この設定をいつでも変更できます。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>SQL Server のインスタンスを自動的に起動するように設定するには  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではないため、新しいバージョンの Windows では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーはアプリケーションとして表示されません。  
    >   
    >  -   **Windows 10**:  
    >          開くには[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager で、**スタート ページ**、SQLServerManager12.msc を入力 (の[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の場合は、12 をより小さい数値に置き換えます。 SQLServerManager12.msc をクリックすると、Configuration Manager が開きます。 スタート ページやタスク バーに構成マネージャーをピン留めする SQLServerManager12.msc を右クリックし、**ファイルの場所を開く**します。 Windows エクスプ ローラーで SQLServerManager12.msc を右クリックし、をクリックし、**スタートにピン留め**または**タスクバーにピン留め**します。  
    > -   **Windows 8**:  
    >          開くには[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager で、**検索**チャームの**アプリ**、型**SQLServerManager\<バージョン > .msc** など`SQLServerManager12.msc`、キーを押しますと**Enter**します。  
  
2.  **[SQL Server 構成マネージャー]** で **[サービス]** を展開し、 **[SQL Server]** をクリックします。  
  
3.  詳細ペインで、自動的に開始するインスタンスの名前を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[SQL Server \<***instancename***> のプロパティ]** ダイアログ ボックスで、 **[開始モード]** を **[自動]** に設定します。  
  
5.  **[OK]** をクリックして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを閉じます。  
  
## <a name="see-also"></a>参照  
 [SQL Server のインスタンスの自動開始の回避 &#40;SQL Server 構成マネージャー&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [別のコンピューターへの接続 &#40;SQL Server 構成マネージャー&#41;](scm-services-connect-to-another-computer.md)   
 [SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
