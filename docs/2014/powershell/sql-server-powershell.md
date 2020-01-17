---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: acfa87245449566c1f91b447910f5194eda192b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922586"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] は、Windows PowerShell をサポートしています。これは、管理者および開発者がサーバー管理やアプリケーション配置を自動化できる強力なスクリプティング シェルです。 Windows PowerShell 言語では [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプトよりも複雑なロジックがサポートされ、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理者は堅牢な管理スクリプトを構築できます。 Windows PowerShell スクリプトは他の [!INCLUDE[msCoName](../includes/msconame-md.md)] サーバー製品の管理にも使用できます。 そのため、管理者はサーバー間で共通のスクリプト言語を使用できるようになります。  
  
## <a name="sql-server-powershell-components"></a>SQL Server PowerShell のコンポーネント  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には、`sqlps` という Windows PowerShell モジュールが用意されており、これを使用して Windows PowerShell 2.0 環境またはスクリプトに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントをインポートします。 `sqlps` モジュールは、以下のものを実装する 2 つの Windows PowerShell スナップインを読み込みます。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダー。プロバイダーを使用すると、ファイル システム パスと同様の簡単なナビゲーション メカニズムを使用できます。 ファイル システム パスと同様に、ドライブが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト モデルに関連付けられ、ノードがオブジェクト モデルのクラスに基づくパスを構築できます。 その後、 **cd** や **dir** などのなじみのあるコマンドを使用して、コマンド プロンプト ウィンドウでフォルダーを操作するのと同様の方法でパスを操作できます。 **ren** や **del**などの他のコマンドを使用すると、パスのノードで操作を実行できます。  
  
-   コマンドレットのセット。Windows PowerShell スクリプトで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の操作を指定するために使用されるコマンドです。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コマンドレットは、[!INCLUDE[tsql](../includes/tsql-md.md)] または XQuery ステートメントを含む **sqlcmd** スクリプトの実行などの操作をサポートします。  
  
 Windows PowerShell について学習するには、「[Windows PowerShell ファースト ステップ ガイド](https://msdn.microsoft.com/library/hh857337.aspx)」を参照してください。  
  
## <a name="sql-server-versions"></a>SQL Server のバージョン  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerShell コンポーネントを使用して管理できるのは、 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] 以降のインスタンスです。 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] のインスタンスは、SP2 以降を実行している必要があります。 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] のインスタンスは、SP4 以降を実行している必要があります。 以前のバージョンの [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]PowerShell コンポーネントを使用した場合、その機能は、以前のバージョンで利用できる機能に限定されます。  
  
## <a name="sql-server-powershell-tasks"></a>SQL Server PowerShell のタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|PowerShell セッションを開き、`sqlps` モジュールを読み込むという、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell コンポーネントを実行するための推奨メカニズムについて説明します。 `sqlps` モジュールは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell プロバイダーおよびコマンドレットと、それらによって使用される SQL Server 管理オブジェクト (SMO) アセンブリを読み込みます。|[SQLPS モジュールのインポート](../database-engine/import-the-sqlps-module.md)|  
|プロバイダーもコマンドレットも読み込まず、SMO アセンブリだけを読み込む方法について説明します。|[Windows PowerShell への SMO アセンブリの読み込み](load-the-smo-assemblies-in-windows-powershell.md)|  
|**オブジェクト エクスプローラー**でノードを右クリックすることによって Windows PowerShell セッションを実行する方法について説明します。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] によって Windows PowerShell セッションが起動され、`sqlps` モジュールが読み込まれて、選択したオブジェクトへの SQL Server プロバイダー パスが設定されます。|[SQL Server Management Studio からの Windows PowerShell の実行](run-windows-powershell-from-sql-server-management-studio.md)|  
|Windows PowerShell スクリプトを実行する SQL Server エージェントのジョブ ステップを作成する方法について説明します。 ジョブは、特定の時刻に実行したり、イベントに応答して実行したりするように設定できます。|[SQL Server エージェントでの Windows PowerShell ステップの実行](run-windows-powershell-steps-in-sql-server-agent.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オブジェクトの階層を移動するために [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーを使用する方法について説明します。|[SQL Server PowerShell プロバイダー](sql-server-powershell-provider.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] スクリプトの実行などの [!INCLUDE[ssDE](../includes/ssde-md.md)] 操作を指定する [!INCLUDE[tsql](../includes/tsql-md.md)] コマンドレットを使用する方法について説明します。|[データベース エンジン コマンドレットの使用](../database-engine/use-the-database-engine-cmdlets.md)|  
|Windows PowerShell でサポートされていない文字を含む、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の区切られた識別子を指定する方法について説明します。|[PowerShell での SQL Server 識別子](sql-server-identifiers-in-powershell.md)|  
|SQL Server 認証接続を確立する方法について説明します。 既定では、SQL Server PowerShell コンポーネントは、Windows PowerShell を実行しているプロセスの Windows 資格情報を使用する Windows 認証接続を使用します。|[データベース エンジン PowerShell での認証の管理](manage-authentication-in-database-engine-powershell.md)|  
|Windows PowerShell のタブ補完を使用する場合に一覧に表示されるオブジェクトの数を制御するために、SQL Server PowerShell プロバイダーによって実装されている変数を使用する方法について説明します。 これは、多数のオブジェクトを含むデータベースで作業する場合に、特に便利です。|[タブ補完の管理 &#40;SQL Server PowerShell&#41;](manage-tab-completion-sql-server-powershell.md)|  
|Windows PowerShell 環境で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントの情報を取得するために Get-Help を使用する方法について説明します。|[SQL Server PowerShell のヘルプの参照](../database-engine/get-help-sql-server-powershell.md)|  
  
  
