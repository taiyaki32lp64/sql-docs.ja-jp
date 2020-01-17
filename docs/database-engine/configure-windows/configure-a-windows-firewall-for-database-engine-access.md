---
title: データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], firewall systems
- firewall systems, [Database Engine]
- security [SQL Server], firewalls
ms.assetid: 0093b43c-c6b5-4574-9b30-3a0e91e1a1f9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d3ec56a8e4961985a6c809983f671edf0234491d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012889"
---
# <a name="configure-a-windows-firewall-for-database-engine-access"></a>データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で SQL Server 構成マネージャーを使用して、データベース エンジン アクセスのための Windows ファイアウォールを構成する方法について説明します。 ファイアウォール システムは、コンピューター リソースへの不正アクセスを防ぐのに役立ちます。 ファイアウォールを経由して [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスにアクセスするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターで、アクセスを許可するようにファイアウォールを構成する必要があります。  
  
 Windows ファイアウォールの既定の設定の詳細と、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、Analysis Services、Reporting Services、および Integration Services に影響する TCP ポートの説明については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご覧ください。 多くのファイアウォール システムが市販されています。 システム固有の情報については、ファイアウォールのマニュアルを参照してください。  
  
 アクセスを許可するための主な手順を次に示します。  
  
1.  特定の TCP/IP ポートを使用するように [!INCLUDE[ssDE](../../includes/ssde-md.md)] を構成します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の既定のインスタンスはポート 1433 を使用しますが、使用するポートは変更できます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] で使用されているポートは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに記録されます。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] と [!INCLUDE[ssEW](../../includes/ssew-md.md)] のインスタンス、および[!INCLUDE[ssDE](../../includes/ssde-md.md)]の名前付きインスタンスは動的ポートを使用します。 特定のポートを使うようにこれらのインスタンスを構成する方法については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)」をご覧ください。  
  
2.  認証済みのユーザーまたはコンピューターが上記で構成したポートにアクセスできるように、ファイアウォールを構成します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを使用すると、ユーザーはポート番号を意識することなく、ポート 1433 でリッスンしていない [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser を使用するには、UDP ポート 1434 を開く必要があります。 環境のセキュリティを最大限に強化するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを停止した状態で、ポート 1434 を使用して接続するようにクライアントを構成します。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows では、既定で Windows ファイアウォールが有効になっており、ポート 1433 が閉じられ、インターネットからコンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスに接続できない状態になっています。 TCP/IP を使用して既定のインスタンスに接続するには、再度ポート 1433 を開く必要があります。 Windows ファイアウォールの基本的な構成手順を次に示します。 詳細については、Windows のマニュアルを参照してください。  
  
 上記の方法のように、特定のポートでリッスンするように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成してそのポートを開く代わりに、ブロックするプログラムの例外の一覧に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の実行可能ファイル (Sqlservr.exe) を追加することもできます。 この方法は、引き続き動的ポートを使用するときに使用します。 この方法でアクセスできる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは 1 つだけです。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **データベース エンジン アクセスを有効にするように Windows ファイアウォールを構成するには、次のものを使用します。**  
  
     [SQL Server 構成マネージャー](#SSMSProcedure)  
  
## <a name="before-you-begin"></a>はじめに  
  
###  <a name="Security"></a> セキュリティ  
 ファイアウォールのポートを開くと、サーバーが攻撃を受けやすくなります。 ポートを開く前に、ファイアウォール システムについて理解しておいてください。 詳細については、「 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)」をご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
 Windows Vista、Windows 7、および Windows Server 2008 に適用されます。  
  
 次の手順では、セキュリティが強化された Windows ファイアウォールの Microsoft 管理コンソール (MMC) スナップインを使用して Windows ファイアウォールを構成します。 セキュリティが強化された Windows ファイアウォールでは、現在のプロファイルのみを構成できます。 セキュリティが強化された Windows ファイアウォールの詳細については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご覧ください。  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access"></a>TCP アクセス用に Windows ファイアウォールのポートを開くには  
  
1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックして **「WF.msc」** と入力し、 **[OK]** をクリックします。  
  
2.  **[セキュリティが強化された Windows ファイアウォール]** の左ペインの **[受信の規則]** をクリックし、[操作] ペインの **[新規の規則]** をクリックします。  
  
3.  **[規則の種類]** ダイアログ ボックスで、 **[ポート]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[プロトコルおよびポート]** ダイアログ ボックスで、 **[TCP]** をクリックします。 **[特定のローカル ポート]** をクリックし、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスのポート番号を入力します。たとえば、既定のインスタンスの場合は「 **1433** 」と入力します。 **[次へ]** をクリックします。  
  
5.  **[操作]** ダイアログ ボックスで、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
6.  **[プロファイル]** ダイアログ ボックスで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続するときのコンピューター接続環境を表すプロファイルをすべて選択し、 **[次へ]** をクリックします。  
  
7.  **[名前]** ダイアログ ボックスで、この規則の名前と説明を入力し、 **[完了]** をクリックします。  
  
#### <a name="to-open-access-to-sql-server-when-using-dynamic-ports"></a>動的ポートの使用時に SQL Server にアクセスするには  
  
1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックして **「WF.msc」** と入力し、 **[OK]** をクリックします。  
  
2.  **[セキュリティが強化された Windows ファイアウォール]** の左ペインの **[受信の規則]** をクリックし、[操作] ペインの **[新規の規則]** をクリックします。  
  
3.  **[規則の種類]** ダイアログ ボックスで、 **[プログラム]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[プログラム]** ダイアログ ボックスで、 **[このプログラムのパス]** をクリックします。 **[参照]** をクリックし、ファイアウォール経由でアクセスする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに移動して、 **[開く]** をクリックします。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Sqlservr.exe**にあります。 **[次へ]** をクリックします。  
  
5.  **[操作]** ダイアログ ボックスで、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
6.  **[プロファイル]** ダイアログ ボックスで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続するときのコンピューター接続環境を表すプロファイルをすべて選択し、 **[次へ]** をクリックします。  
  
7.  **[名前]** ダイアログ ボックスで、この規則の名前と説明を入力し、 **[完了]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [方法: ファイアウォール設定を構成する (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
