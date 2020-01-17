---
title: 別のコンピューターへの接続 (SQL Server 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], other computers
ms.assetid: c4c1e94f-4f5f-431e-8b5b-d5ff97baf723
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4305438285ae5f3b51ab8ac51ec2b1d0699aee64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810350"
---
# <a name="connect-to-another-computer-sql-server-configuration-manager"></a>別のコンピューターへの接続 (SQL Server 構成マネージャー)
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で別のコンピューターに接続する方法について説明します。 Windows の [コンピューターの管理] の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) を開くための最初の手順に従って、コンピューターに接続し、[サービスとアプリケーション] ツリーを展開します。 2 番目の手順に従って、リモート コンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーへのリンクを含むファイルを作成します。  
  
> [!NOTE]  
>  リモートで接続している場合、一部の操作は構成マネージャーで実行することができません。  
  
 別のコンピューターのサービスを開始、停止、一時停止、または再開するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してサーバーに接続し、サーバーまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを右クリックし、次に目的の操作をクリックします。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-connect-to-another-computer-with-windows-computer-management"></a>Windows のコンピューターの管理を使用して別のコンピューターに接続するには  
  
1.  **[スタート]** メニューで **[マイ コンピューター]** を右クリックし、 **[管理]** をクリックします。  
  
2.  **[コンピューターの管理]** で **[コンピューターの管理 (ローカル)]** を右クリックし、 **[別のコンピューターへ接続]** をクリックします。  
  
3.  **[コンピューターの選択]** ダイアログ ボックスの **[別のコンピューター]** ボックスに管理するコンピューターの名前を入力し、 **[OK]** をクリックします。  
  
     リモート コンピューターで実行されているサービスが、[コンピューターの管理] に表示されます。 最上位ノードが **[コンピューターの管理 \<*remotecomputer*>]** に変更されます。  
  
4.  コンソール ツリーの **[サービスとアプリケーション]** を展開し、 **[SQL Server 構成マネージャー]** を展開して、リモート コンピューターのサービスを管理します。  
  
#### <a name="to-save-a-link-to-sql-server-configuration-manager-for-another-computer"></a>別のコンピューターの SQL Server 構成マネージャーへのリンクを保存するには  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。  
  
2.  **開く**ボックスに「`mmc -a`を開く、[!INCLUDE[msCoName](../../includes/msconame-md.md)]管理コンソールを作成者モードでします。  
  
3.  **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。  
  
4.  **[スナップインの追加と削除]** ウィンドウで **[追加]** をクリックします。  
  
5.  **[スタンドアロン スナップインの追加]** ウィンドウで **[コンピューターの管理]** をクリックし、次に **[追加]** をクリックします。  
  
6.  **[コンピューターの管理]** ウィンドウの **[別のコンピューター]** をクリックし、管理するリモート コンピューターの名前を入力して **[完了]** をクリックします。  
  
7.  **[スタンドアロン スナップインの追加]** ウィンドウで **[閉じる]** をクリックします。  
  
8.  **[スナップインの追加と削除]** ウィンドウで **[OK]** をクリックします。  
  
9. **[コンピューターの管理 (***\<コンピューター名>***)]** 、 **[サービスとアプリケーション]** の順に展開します。  
  
10. **[SQL Server 構成マネージャー]** を右クリックして、 **[ここから新しいウィンドウ]** をクリックします。  
  
11. **[ウィンドウ]** メニューの **[コンソール ルート]** をクリックし、最初のウィンドウに切り替えてからそのウィンドウを削除します。  
  
12. **ファイル** メニューのをクリックして**名前を付けて保存**で適切な名前で、目的のフォルダーにファイルを保存し、`.msc`ファイル拡張子。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソールを閉じます。  
  
13. ターゲット コンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、そのファイルをダブルクリックします。 必要な場合は、デスクトップまたは **[スタート]** メニューにファイルへのリンクを保存します。  
  
> [!CAUTION]  
>  リモート コンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用する場合、コンピューター名が明らかではないため、誤って別のコンピューターを停止または構成してしまう可能性があります。 サービスを変更する前に、 **[サービス]** タブの **[ホスト名]** ボックスを調べてコンピューター名を確認してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
