---
title: サーバー監査およびサーバー監査の仕様を作成する方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.SQLAUDIT.FILTER.F1
- sql12.swb.sqlaudit.srvaudit.general.f1
- sql12.swb.sqlaudit.general.f1
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
ms.assetid: 6624b1ab-7ec8-44ce-8292-397edf644394
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ec1c7205597224e5fca27942ca25ad4e197ec0d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198412"
---
# <a name="create-a-server-audit-and-server-audit-specification"></a>サーバー監査およびサーバー監査の仕様を作成する方法
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、サーバー監査またはサーバー監査仕様を作成する方法について説明します。 *のインスタンスや* データベースの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、システムで発生するイベントの追跡およびログ記録が行われます。 *SQL Server Audit* オブジェクトは、監視するサーバー レベルまたはデータベース レベルのアクションおよびアクションのグループの 1 つのインスタンスを収集します。 監査は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス レベルで行われます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスごとに複数の監査を使用できます。 *サーバー監査の仕様* オブジェクトは監査に属しています。 サーバー監査の仕様は監査ごとに 1 つ作成できます。これは、サーバー監査の仕様も監査も [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのスコープで作成されるためです。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](sql-server-audit-database-engine.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **次のものを使用してサーバー監査およびサーバー監査の仕様を作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   サーバー監査仕様を作成するには、対象の監査が事前に存在している必要があります。 サーバー監査仕様は作成されたとき無効な状態です。  
  
-   CREATE SERVER AUDIT ステートメントはトランザクションのスコープ内にあります。 トランザクションがロールバックされると、ステートメントもロールバックされます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
  
-   サーバー監査を作成、変更、または削除する場合、プリンシパルには、ALTER ANY SERVER AUDIT または CONTROL SERVER の権限が必要です。  
  
-   ALTER ANY SERVER AUDIT 権限を持つユーザーは、サーバー監査の仕様を作成し、任意の監査にバインドできます。  
  
-   サーバー監査仕様の作成後は、CONTROL SERVER または ALTER ANY SERVER AUDIT 権限を持つプリンシパル、sysadmin アカウント、またはその監査への明示的なアクセス権を持つプリンシパルがその仕様を表示できます。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-server-audit"></a>サーバー監査を作成するには  
  
1.  オブジェクト エクスプローラーで、 **[セキュリティ]** フォルダーを展開します。  
  
2.  **[監査]** フォルダーを右クリックし、 **[新しい監査]** を選択します。  
  
     **[監査の作成]** ダイアログ ボックスの **[全般]** ページでは、次のオプションを使用できます。  
  
     **[監査名]**  
     監査の名前。 これは、新しい監査を作成すると自動的に生成されますが、編集可能です。  
  
     **[処理の遅延 (ミリ秒)]**  
     監査アクションの処理が強制されるまでの時間 (ミリ秒単位) を指定します。  値 0 は同期配信を表します。 既定の最小値は **1000** (1 秒) です。 最大値は 2,147,483,647 (2,147,483.647 秒、つまり 24 日、20 時間、31 分、23.647 秒) です。  
  
     **[監査ログ エラー発生時]**  
     **Continue**  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 操作を続行します。 監査レコードは保持されません。 監査はイベントのログ記録を試行し続け、エラー状態が解決されると、記録を再開します。 **[続行]** オプションを選択すると、セキュリティ ポリシーに違反する可能性がある、監査されない活動を許すおそれがあります。 完全な監査を維持することより、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の操作を続行することの方が重要である場合に、このオプションを選択します。 これは既定値です。  
  
     **[サーバーのシャットダウン]**  
     監査対象に書き込みを行うサーバー インスタンスが監査対象にデータを書き込むことができない場合に、サーバーを強制的にシャットダウンします。 これを発行するログインには、`SHUTDOWN` 権限が必要です。 ログオンにこの権限がない場合、この機能は失敗し、エラー メッセージが表示されます。 監査イベントは発生しません。 監査エラーによってシステムのセキュリティまたは整合性が阻害される可能性がある場合に、このオプションを選択します。  
  
     **[失敗の操作]**  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit が監査ログを出力できないとき、そのままではデータベース アクションが原因で、監査イベントが発生する場合、そのデータベース アクションを失敗させます。 監査イベントは発生しません。 監査イベントを発生させないアクションは続行できます。 監査はイベントのログ記録を試行し続け、エラー状態が解決されると、記録を再開します。 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]へのフル アクセスより、完全な監査の維持の方が重要である場合に、このオプションを選択します。  
  
    > [!IMPORTANT]  
    >  監査が失敗状態のとき、専用管理者接続は、監査イベントの実行を継続できます。  
  
     **[監査の出力先]** の一覧  
     監査データの出力先を指定します。 バイナリ ファイル、Windows アプリケーション ログ、または Windows セキュリティ ログを指定できます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、Windows で追加の設定を行わないと Windows セキュリティ ログに書き込むことができません。 詳細については、「 [セキュリティ ログへの SQL サーバー監査イベントの書き込み](write-sql-server-audit-events-to-the-security-log.md)」を参照してください。  
  
     **[ファイル パス]**  
     **[監査の出力先]** にファイルが指定されている場合に、監査データが書き込まれるフォルダーの場所を指定します。  
  
     **省略記号 (...)**  
     開く、**フォルダーの検索 -** _server_name_ファイル パスを指定したり監査ファイルの書き込み先フォルダーを作成 ダイアログ ボックス。  
  
     **[監査ファイルの最大限度]**  
     **[ロールオーバー ファイルの最大数]**  
     監査ファイルがその最大数に達すると、最も古い監査ファイルが新しいファイルの内容で上書きされることを指定します。  
  
     **[最大ファイル]**  
     監査ファイル数が上限に達すると、追加の監査イベントを生成させるアクションが失敗し、エラーが発生することを指定します。  
  
     **[無制限]** チェック ボックス  
     **[ロールオーバー ファイルの最大数]** の **[無制限]** チェック ボックスがオンの場合、作成される監査ファイルの数は制限されません。 **[無制限]** チェック ボックスは既定でオンになり、 **[ロールオーバー ファイルの最大数]** と **[最大ファイル数]** の両方の選択に適用されます。  
  
     **[ファイルの数]** ボックス  
     作成する監査ファイル数を指定します (2,147,483,647 まで)。 このオプションは、 **[無制限]** がオフの場合にのみ利用可能です。  
  
     **[最大ファイル サイズ]**  
     監査ファイルの最大サイズをメガバイト (MB)、ギガバイト (GB)、またはテラバイト (TB) 単位で指定します。 1024 MB ～ 2,147,483,647 TB の範囲で指定できます。 **[無制限]** チェック ボックスをオンにした場合、ファイルのサイズに制限は設定されません。 1024 MB 未満の値を指定すると、失敗し、エラーが返されます。 既定では、 **[無制限]** チェック ボックスはオンになっています。  
  
     **[ディスク領域を予約する]** チェック ボックス  
     指定した最大ファイル サイズと等しい領域が、ディスク上に事前に割り当てられるように指定します。 この設定は、 **[最大ファイル サイズ]** の **[無制限]** チェック ボックスがオフの場合にのみ使用できます。 既定では、このチェック ボックスはオフになっています。  
  
3.  オプションで、 **[フィルター]** ページでサーバー監査に対する述語または `WHERE` 句を入力して、 **[全般]** ページからは使用できない追加オプションを指定します。 述語はかっこで囲みます。たとえば、 `(object_name = 'EmployeesTable')`と指定します。  
  
4.  オプションの選択が完了したら、 **[OK]** をクリックします。  
  
#### <a name="to-create-a-server-audit-specification"></a>サーバー監査仕様を作成するには  
  
1.  オブジェクト エクスプローラーで、プラス記号をクリックして **[セキュリティ]** フォルダーを展開します。  
  
2.  **[サーバー監査の仕様]** フォルダーを右クリックし、 **[新しいサーバー監査の仕様]** を選択します。  
  
     **[サーバー監査の仕様の作成]** ダイアログ ボックスで、次のオプションを使用できます。  
  
     **名前**  
     サーバー監査の仕様の名前。 この名前は、新しいサーバー監査の仕様を作成すると自動的に生成されますが、編集可能です。  
  
     **監査**  
     既存のサーバー監査の名前。 監査の名前を入力するか、一覧から選択します。  
  
     **[監査アクションの種類]**  
     キャプチャするサーバー レベルの監査アクション グループと監査アクションを指定します。 サーバー レベルの監査アクション グループと監査アクションの一覧、およびそれらに含まれるイベントの説明については、「 [SQL Server 監査のアクション グループとアクション](sql-server-audit-action-groups-and-actions.md)」を参照してください。  
  
     **[オブジェクト スキーマ]**  
     指定した **[オブジェクト名]** のスキーマを表示します。  
  
     **[オブジェクト名]**  
     監査するオブジェクトの名前。 これは監査アクションにのみ使用できます。監査グループには適用されません。  
  
     **省略記号 (...)**  
     指定した **[監査アクションの種類]** に基づいて、使用可能なオブジェクトを参照して選択するための **[オブジェクトの選択]** ダイアログ ボックスを開きます。  
  
     **[プリンシパル名]**  
     監査対象のオブジェクトで監査をフィルター選択するためのアカウント。  
  
     **省略記号 (...)**  
     指定した **[オブジェクト名]** に基づいて、使用可能なオブジェクトを参照して選択するための **[オブジェクトの選択]** ダイアログ ボックスを開きます。  
  
3.  終了したら **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-server-audit"></a>サーバー監査を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Creates a server audit called "HIPAA_Audit" with a binary file as the target and no options.  
    CREATE SERVER AUDIT HIPAA_Audit  
        TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
    ```  
  
#### <a name="to-create-a-server-audit-specification"></a>サーバー監査仕様を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    /*Creates a server audit specification called "HIPAA_Audit_Specification" that audits failed logins for the SQL Server audit "HIPAA_Audit" created above.  
    */  
  
    CREATE SERVER AUDIT SPECIFICATION HIPAA_Audit_Specification  
    FOR SERVER AUDIT HIPAA_Audit  
        ADD (FAILED_LOGIN_GROUP);  
    GO  
    -- Enables the audit.   
  
    ALTER SERVER AUDIT HIPAA_Audit  
    WITH (STATE = ON);  
    GO  
    ```  
  
 詳細については、「[CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql)」および「[CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-specification-transact-sql)」を参照してください。  
  
  
