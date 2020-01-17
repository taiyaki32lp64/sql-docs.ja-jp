---
title: Transact-SQL デバッガーの構成
ms.custom: seo-lt-2019
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.error.sqlde_register_failed
- vs.debug.error.sqlde_accessdenied
- vs.debug.error.sqlde_firewall.remotemachines
helpviewer_keywords:
- Transact-SQL debugger, remote connections
- Windows Firewall [Database Engine], Transact-SQL debugger
- Transact-SQL debugger, Windows Firewall
- Transact-SQL debugger, configuring
- ports [SQL Server], Transact-SQL debugger
- TCP/IP [SQL Server], port numbers
ms.assetid: f50e0b0d-eaf0-4f4a-be83-96f5be63e7ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60d5af2752a426faca3069541deeae3a6aa4f495
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245190"
---
# <a name="configure-the-transact-sql-debugger"></a>Transact-SQL デバッガーの構成
  
  [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディターとは別のコンピューター上で動作する [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに接続するときに [!INCLUDE[ssDE](../../includes/ssde-md.md)] デバッグを有効にするように Windows ファイアウォール規則を構成する必要があります。  
  
## <a name="configuring-the-transact-sql-debugger"></a>Transact-SQL デバッガーの構成  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーには、サーバー側のコンポーネントとクライアント側のコンポーネントの両方が含まれています。 サーバー側のデバッガー コンポーネントは、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 (SP2) 以降のデータベース エンジンの各インスタンスと共にインストールされます。 クライアント側のデバッガー コンポーネントは、以下の時点で含まれます。  
  
-   
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降からクライアント側のツールをインストールするとき。  
  
-   microsoft visual studio 2010 以降をインストールするとき。  
  
-   Web ダウンロードから [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] をインストールするとき。  
  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] が [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] インスタンスと同じコンピューター上で実行されている場合は、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]デバッガーを実行するための構成要件はありません。 ただし、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のリモート インスタンスに接続するときに [!INCLUDE[ssDE](../../includes/ssde-md.md)]デバッガーを実行するには、Windows ファイアウォールのプログラムとポートの規則を両方のコンピューターで有効にする必要があります。 これらの規則は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップによって作成できます。 リモート デバッグ セッションを開こうとしたときにエラーが発生する場合は、次のファイアウォール規則がコンピューターに定義されていることを確認します。  
  
 ファイアウォール規則を管理するには、 **セキュリティが強化された Windows ファイアウォール** アプリケーションを使用します。 
  [!INCLUDE[win7](../../includes/win7-md.md)] と [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]のどちらの場合でも、 **[コントロール パネル]** を開き、 **[Windows ファイアウォール]** を開いて **[詳細設定]** をクリックします。 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] では、 **[サービス マネージャー]** を開き、左側のペインで **[構成]** を展開し、 **[セキュリティが強化された Windows ファイアウォール]** を展開することもできます。  
  
> [!CAUTION]  
>  Windows ファイアウォール規則を有効にした場合、ファイアウォールでブロックするように指定されているセキュリティ上の脅威にコンピューターがさらされる可能性があります。 リモート デバッグ用の規則を有効にすると、このトピックで示されているポートとプログラムのブロックが解除されます。  
  
## <a name="firewall-rules-on-the-server"></a>サーバー上のファイアウォール規則  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスが実行されているコンピューター上で、 **セキュリティが強化された Windows ファイアウォール** を使用して、次の情報を指定します。  
  
-   sqlservr.exe の受信プログラム規則を追加します。 リモート デバッグ セッションをサポートする必要がある各インスタンス用の規則が必要です。  
  
    1.  
  **[セキュリティが強化された Windows ファイアウォール]** で、左側のペインの **[受信の規則]** をクリックし、[操作] ペインの **[新しい規則]** をクリックします。  
  
    2.  
  **[規則の種類]** ダイアログで、 **[プログラム]** をクリックし、 **[次へ]** をクリックします。  
  
    3.  
  **[プログラム]** ダイアログで、 **[このプログラムのパス:]** をクリックし、このインスタンスの sqlservr.exe の完全なパスを入力します。 既定では、sqlservr.exe は C:\Program ・ SQL Server\MSSQL12. にインストールされます。*Instancename*\MSSQL\Binn。 *instancename*は既定のインスタンスの場合は MSSQLSERVER、名前付きインスタンスの場合はインスタンス名です。  
  
    4.  
  **[操作]** ダイアログで、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
    5.  
  **[プロファイル]** ダイアログで、インスタンスとのデバッグ セッションを開くときのコンピューター接続環境を表すプロファイルをすべて選択し、 **[次へ]** をクリックします。  
  
    6.  
  **[名前]** ダイアログで、この規則の名前と説明を入力し、 **[完了]** をクリックします。  
  
    7.  
  **[受信の規則]** の一覧で、作成した規則を右クリックし、[操作] ペインの **[プロパティ]** を選択します。  
  
    8.  
  **[プロトコルおよびポート]** タブをクリックします。  
  
    9. 
  **[プロトコルの種類:]** ボックスで **[TCP]** 、 **[ローカル ポート:]** ボックスで **[RPC 動的ポート]** を選択します。次に、 **[適用]** をクリックし、 **[OK]** をクリックします。  
  
-   svchost.exe の受信プログラム規則を追加して、リモート デバッグ セッションからの DCOM 通信を有効にします。  
  
    1.  
  **[セキュリティが強化された Windows ファイアウォール]** で、左側のペインの **[受信の規則]** をクリックし、[操作] ペインの **[新しい規則]** をクリックします。  
  
    2.  
  **[規則の種類]** ダイアログで、 **[プログラム]** をクリックし、 **[次へ]** をクリックします。  
  
    3.  
  **[プログラム]** ダイアログで、 **[このプログラムのパス:]** をクリックし、svchost.exe の完全なパスを入力します。 既定では、svchost.exe は %systemroot%\System32\svchost.exe にインストールされます。  
  
    4.  
  **[操作]** ダイアログで、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
    5.  
  **[プロファイル]** ダイアログで、インスタンスとのデバッグ セッションを開くときのコンピューター接続環境を表すプロファイルをすべて選択し、 **[次へ]** をクリックします。  
  
    6.  
  **[名前]** ダイアログで、この規則の名前と説明を入力し、 **[完了]** をクリックします。  
  
    7.  
  **[受信の規則]** の一覧で、作成した規則を右クリックし、[操作] ペインの **[プロパティ]** を選択します。  
  
    8.  
  **[プロトコルおよびポート]** タブをクリックします。  
  
    9. 
  **[プロトコルの種類:]** ボックスで **[TCP]** 、 **[ローカル ポート:]** ボックスで **[RPC エンドポイント マッパー]** を選択します。次に、 **[適用]** をクリックし、 **[OK]** をクリックします。  
  
-   ドメイン ポリシーにより IPSec 経由でネットワーク通信を行う必要がある場合は、UDP ポート 4500 と UDP ポート 500 を開く受信規則も追加する必要があります。  
  
## <a name="firewall-rules-on-the-client"></a>クライアント上のファイアウォール規則  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターを実行中のコンピューターでは、SQL Server セットアップまたは [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] セットアップで Windows ファイアウォールがリモート デバッグを許可するように構成されている場合があります。  
  
 リモート デバッグ セッションを開こうとしたときにエラーが発生する場合は、 **セキュリティが強化された Windows ファイアウォール** を使用してファイアウォール規則を構成することで、プログラムとポートの例外を手動で構成できます。  
  
-   svchost 用のプログラム エントリを追加します。  
  
    1.  
  **[セキュリティが強化された Windows ファイアウォール]** で、左側のペインの **[受信の規則]** をクリックし、[操作] ペインの **[新しい規則]** をクリックします。  
  
    2.  
  **[規則の種類]** ダイアログで、 **[プログラム]** をクリックし、 **[次へ]** をクリックします。  
  
    3.  
  **[プログラム]** ダイアログで、 **[このプログラムのパス:]** をクリックし、svchost.exe の完全なパスを入力します。 既定では、svchost.exe は %systemroot%\System32\svchost.exe にインストールされます。  
  
    4.  
  **[操作]** ダイアログで、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
    5.  
  **[プロファイル]** ダイアログで、インスタンスとのデバッグ セッションを開くときのコンピューター接続環境を表すプロファイルをすべて選択し、 **[次へ]** をクリックします。  
  
    6.  
  **[名前]** ダイアログで、この規則の名前と説明を入力し、 **[完了]** をクリックします。  
  
    7.  
  **[受信の規則]** の一覧で、作成した規則を右クリックし、[操作] ペインの **[プロパティ]** を選択します。  
  
    8.  
  **[プロトコルおよびポート]** タブをクリックします。  
  
    9. 
  **[プロトコルの種類:]** ボックスで **[TCP]** 、 **[ローカル ポート:]** ボックスで **[RPC エンドポイント マッパー]** を選択します。次に、 **[適用]** をクリックし、 **[OK]** をクリックします。  
  
-   
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターをホストするアプリケーション用のプログラム エントリを追加します。 同じコンピューター上の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] と [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] からリモート デバッグ セッションを開く必要がある場合は、両方に対してプログラム規則を追加する必要があります。  
  
    1.  
  **[セキュリティが強化された Windows ファイアウォール]** で、左側のペインの **[受信の規則]** をクリックし、[操作] ペインの **[新しい規則]** をクリックします。  
  
    2.  
  **[規則の種類]** ダイアログで、 **[プログラム]** をクリックし、 **[次へ]** をクリックします。  
  
    3.  
  **[プログラム]** ダイアログで、 **[このプログラムのパス:]** をクリックし、次の 3 つの値のいずれかを入力します。  
  
        -   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、ssms.exe の完全パスを入力します。 既定では、ssms.exe は C:\Program Files (x86)\Microsoft SQL Server\120\Tools\Binn\Management Studio にインストールされます。  
  
        -   
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] では、devenv.exe の完全パスを入力します。  
  
            1.  既定では、Visual Studio 2010 用の devenv.exe は、C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE に配置されます。  
  
            2.  既定では、Visual Studio 2012 用の devenv.exe は、C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE に配置されます。  
  
            3.  
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動するために使用するショートカットで、ssms.exe のパスを確認できます。 
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]を起動するために使用するショートカットで、devenv.exe のパスを確認できます。 ショートカットを右クリックし、 **[プロパティ]** をクリックします。 実行可能ファイルとパスが **[ターゲット]** ボックスに表示されます。  
  
    4.  
  **[操作]** ダイアログで、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
    5.  
  **[プロファイル]** ダイアログで、インスタンスとのデバッグ セッションを開くときのコンピューター接続環境を表すプロファイルをすべて選択し、 **[次へ]** をクリックします。  
  
    6.  
  **[名前]** ダイアログで、この規則の名前と説明を入力し、 **[完了]** をクリックします。  
  
    7.  
  **[受信の規則]** の一覧で、作成した規則を右クリックし、[操作] ペインの **[プロパティ]** を選択します。  
  
    8.  
  **[プロトコルおよびポート]** タブをクリックします。  
  
    9. 
  **[プロトコルの種類:]** ボックスで **[TCP]** 、 **[ローカル ポート:]** ボックスで **[RPC 動的ポート]** を選択します。次に、 **[適用]** をクリックし、 **[OK]** をクリックします。  
  
## <a name="requirements-for-starting-the-debugger"></a>デバッガーを起動するための要件  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーを起動するには、次の要件をすべて満たしている必要があります。  
  
* 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] が、sysadmin 固定サーバー ロールのメンバーである Windows アカウントで実行されている必要があります。  
  
* 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが、sysadmin 固定サーバー ロールのメンバーである Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインを使用して接続されている必要があります。  
  
* 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 2 (SP2) 以降の [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のインスタンスに接続されている必要があります。 クエリ エディター ウィンドウがシングル ユーザー モードのインスタンスに接続されているときは、デバッガーを実行できません。

* サーバーとクライアントが RPC 経由で通信をしている必要があります。 SQL Server サービスが実行されているアカウントは、クライアントに対する認証権限を持っている必要があります。  
  
## <a name="see-also"></a>参照  
 [Transact-sql デバッガー](transact-sql-debugger.md)   
 [Transact-sql デバッガーの実行](run-the-transact-sql-debugger.md)   
 [Transact-sql コードのステップ実行](step-through-transact-sql-code.md)   
 [Transact-sql デバッガー情報](transact-sql-debugger-information.md)   
 [データベースエンジンクエリエディター &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)  
  
  
