---
title: データベース エンジン スクリプト | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], PowerShell
- scripts [SQL Server]
- scripting [SQL Server Database Engine]
- scripting [SQL Server Database Engine], PowerShell
ms.assetid: 9978a884-59a2-4e7f-a82a-335149f3a261
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 58a057fbb73008fdab5febd2b9ccdcf07917776d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263520"
---
# <a name="database-engine-scripting"></a>データベース エンジン スクリプト
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] のインスタンスとそのインスタンスに含まれるオブジェクトを管理するための [!INCLUDE[ssDE](../../includes/ssde-md.md)] PowerShell スクリプト環境をサポートします。 スクリプト環境と非常によく似た環境で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] と XQuery を含む [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを作成および実行することもできます。  
  
## <a name="sql-server-powershell"></a>SQL Server PowerShell  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、次を実装する 2 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell スナップインが含まれています。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト モデル階層を、ファイル システム パスと同様の PowerShell パスとして公開する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell プロバイダー。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト モデル クラスを使用して、パスの各ノードで表されるオブジェクトを管理できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コマンドを実装する一連の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コマンドレット。 コマンドレットの 1 つは **Invoke-Sqlcmd**です。 これは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] sqlcmd **ユーティリティで実行される** クエリ スクリプトを実行するために使用されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、PowerShell を実行するための次の機能を備えています。  
  
-   PowerShell セッションにインポートできる **sqlps** PowerShell モジュール。さらにこのモジュールによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スナップインが読み込まれます。アドホック PowerShell コマンドは対話形式で実行できます。 \MyFolder\MyScript.ps1 などのコマンドを使用してスクリプト ファイルを実行できます。  
  
-   PowerShell スクリプト ファイルは、スケジュールされた間隔で、またはシステム イベントに応答してスクリプトを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの PowerShell ジョブ ステップへの入力として使用できます。  
  
-   PowerShell を起動し、 **モジュールをインポートする** sqlps [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ。 これによって、そのモジュールがサポートするすべてのアクションを実行できます。 **sqlps** ユーティリティは、コマンド プロンプトで、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio のオブジェクト エクスプローラー ツリーのノードを右クリックし、 **[PowerShell の起動]** をクリックして開始できます。  
  
## <a name="database-engine-queries"></a>データベース エンジン クエリ  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ スクリプトには、次の 3 種類の要素が含まれます。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語ステートメント  
  
-   XQuery 言語ステートメント  
  
-   **sqlcmd** ユーティリティのコマンドと変数  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリを作成および実行するための次の 3 つの環境を提供します。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] の [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターで [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]クエリを対話形式で実行およびデバッグできます。 1 つのセッションで複数のステートメントをコーディングおよびデバッグしてから、1 つのスクリプト ファイルにすべてのステートメントを保存できます。  
  
-   **sqlcmd** コマンド プロンプト ユーティリティを使用すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリを対話形式で実行できます。また、既存の [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ スクリプト ファイルも実行できます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ スクリプト ファイルは、通常 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターを使用して対話形式でコーディングされます。 ファイルは、次のいずれかの環境で後から開くことができます。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の **[ファイル]** / メニューの **[開く]** を使用して、新しい[!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウでファイルを開きます。  
  
-   **-i**_input_file_ パラメーターを使用して **sqlcmd** ユーティリティでファイルを実行します。  
  
-   **-QueryFromFile** パラメーターを使用して、 **PowerShell スクリプトの** Invoke-Sqlcmd [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コマンドレットでファイルを実行します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップを使用して、スケジュールされた間隔で、またはシステム イベントに応答してスクリプトを実行します。  
  
 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプト生成ウィザードを使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを生成できます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーでオブジェクトを右クリックし、 **[スクリプトの生成]** メニュー項目を選択します。 **[スクリプトの生成]** を選択すると、スクリプトの作成プロセスを支援するウィザードが起動します。  
  
## <a name="database-engine-scripting-tasks"></a>データベース エンジン スクリプトのタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] スクリプトを対話形式で開発、デバッグ、および実行するために、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のコード エディターとテキスト エディターを使用する方法について説明します。|[クエリおよびテキスト エディター &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)|  
|対話形式でスクリプトを開発する機能も含めて、コマンド プロンプトから **スクリプトを実行するために、** sqlcmd [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーティリティを使用する方法について説明します。|[sqlcmd 操作方法のトピック](https://msdn.microsoft.com/library/dd7a2d2b-6327-4d77-ac5a-580d36073ad4)|  
|Windows PowerShell 環境に SQL Server コンポーネントを統合し、SQL Server インスタンスおよびオブジェクトを管理するための PowerShell スクリプトを作成する方法について説明します。|[SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)|  
|データベースの 1 つまたは複数のオブジェクトを再作成する **スクリプトを作成するために、** スクリプトの生成とパブリッシュ [!INCLUDE[tsql](../../includes/tsql-md.md)] ウィザードを使用する方法について説明します。|[スクリプトの生成 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)|  
  
## <a name="see-also"></a>参照  
 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)   
 [チュートリアル: Transact-SQL ステートメントの作成](../../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
