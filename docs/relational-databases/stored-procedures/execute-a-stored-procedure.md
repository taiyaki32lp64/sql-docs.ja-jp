---
title: ストアド プロシージャの実行 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
f1_keywords:
- sql13.swb.executeprocedure.general.f1
- sql13.swb.executeprocedure.f1
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- extended stored procedures [SQL Server], executing
- system stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- user-defined stored procedures [SQL Server]
ms.assetid: a0b1337d-2059-4872-8c62-3f967d8b170f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f088c526666dcd81d269bc68479914202969a2e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934048"
---
# <a name="execute-a-stored-procedure"></a>ストアド プロシージャの実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でストアド プロシージャを実行する方法について説明します。  
  
 ストアド プロシージャを実行するには、2 つの方法があります。 1 つ目の最も一般的な方法は、アプリケーションまたはユーザーがプロシージャを呼び出す方法です。 2 番目の方法は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの起動時にプロシージャが自動的に実行されるように設定する方法です。 アプリケーションまたはユーザーによってプロシージャが呼び出される場合は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] の EXECUTE または EXEC キーワードが呼び出しの中に明示的に指定されています。 または、プロシージャが [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ内の最初のステートメントである場合は、このキーワードを使用せずにストアド プロシージャを呼び出すことができます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **ストアド プロシージャを実行するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   システム プロシージャ名を照合するときに、呼び出し元のデータベースの照合順序が使用されます。 そのため、プロシージャの呼び出しでは、システム プロシージャ名の大文字と小文字を常に区別する必要があります。 たとえば、次のコードは、大文字と小文字を区別する照合順序が指定されたデータベースのコンテキストで実行された場合は失敗します。  
  
    ```sql  
    EXEC SP_heLP; -- Will fail to resolve because SP_heLP does not equal sp_help  
    ```  
  
     正確なシステム ストアド プロシージャ名を表示するには、 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) カタログ ビューおよび [sys.system_parameters](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md) カタログ ビューをクエリします。  
  
-   システム プロシージャと同じ名前を持つユーザー定義プロシージャは、実行されない可能性があります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   システム ストアド プロシージャの実行  
  
     システム ストアド プロシージャは、 **sp_** というプレフィックスで始まります。 それらは論理的にすべてのユーザー定義データベースおよびシステム定義データベースに表示されるため、プロシージャ名を完全修飾する必要なく、任意のデータベースから実行できます。 ただし、名前の競合を回避するためには、すべてのシステム プロシージャ名を **sys** スキーマ名でスキーマ修飾することをお勧めします。 次の例は、システム ストアド プロシージャの呼び出しに関して推奨されている方法を示しています。  
  
    ```sql  
    EXEC sys.sp_who;  
    ```  
  
-   ユーザー定義のストアド プロシージャの実行  
  
     ユーザー定義のプロシージャを実行する場合は、プロシージャ名をスキーマ名で修飾することをお勧めします。 これにより、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が複数のスキーマに対して検索を実行する必要がなくなるため、パフォーマンスが多少向上します。 また、複数のスキーマに同じ名前のプロシージャがあるデータベースで誤ったプロシージャが実行されることを防止できます。  
  
     次の例は、ユーザー定義のプロシージャを実行するために推奨されている方法を示しています。 このプロシージャは 1 つの入力パラメーターを受け取ります。 入力パラメーターと出力パラメーターを指定する方法の詳細については、「 [パラメーターの指定](../../relational-databases/stored-procedures/specify-parameters.md)」を参照してください。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    EXEC dbo.uspGetEmployeeManagers @BusinessEntityID = 50;  
    ```  
  
     または  
  
    ```sql  
    EXEC AdventureWorks2012.dbo.uspGetEmployeeManagers 50;  
    GO  
    ```  
  
     修飾されていないユーザー定義のプロシージャを指定した場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では次の順序でプロシージャが検索されます。  
  
    1.  現在のデータベースの **sys** スキーマ。  
  
    2.  バッチまたは動的 SQL で実行された場合は、呼び出し側の既定のスキーマ。 または、別のプロシージャ定義の本文の中に非修飾型プロシージャ名がある場合は、そのプロシージャを含んでいるスキーマが次に検索されます。  
  
    3.  現在のデータベースの **dbo** スキーマ。  
  
-   ストアド プロシージャの自動実行  
  
     自動実行用にマークされたプロシージャは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動するたびに実行されます。スタートアップ プロセス中に、 **master** データベースが復旧されます。 データベースのメンテナンス操作を実行する場合や、バックグラウンド プロセスとしてプロシージャを連続実行する場合は、自動実行するようにプロシージャを設定すると便利です。 プロシージャの自動実行は、グローバル一時テーブルの作成など、 **tempdb**のシステム タスクまたはメンテナンス タスクを行う場合にも使用できます。 このようにすると、 **のスタートアップ時に** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再作成されても、一時テーブルの存在が保証されます。  
  
     自動実行されるプロシージャは、固定サーバー ロール **sysadmin** と同じ権限で操作を行います。 これらのプロシージャが生成するエラー メッセージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに書き込まれます。  
  
     スタートアップ プロシージャの数に制限はありませんが、実行中、プロシージャ 1 つにつき 1 つのワーカー スレッドが使用されます。 スタートアップ時に複数のプロシージャを実行する場合でも、並列に実行する必要がないときは 1 つのプロシージャをスタートアップ プロシージャとし、そのプロシージャが残りのプロシージャを呼び出すようにします。 この場合は、全体で 1 つのワーカー スレッドしか使用されません。  
  
    > [!TIP]  
    >  自動実行されるプロシージャからは、結果セットを返さないでください。 自動実行されるプロシージャは、アプリケーションやユーザーではなく [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行するので、結果セットを返す先がないためです。  
  
-   自動実行の設定、解除、および制御  
  
     自動実行されるようにプロシージャを設定できるのは、システム管理者 (**sa**) だけです。 また、このプロシージャは、 **master** データベースに格納されていて、 **sa**により所有されている必要があり、入出力パラメーターを受け渡すことはできません。  
  
     次の操作を実行するには、 [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) を使用します。  
  
    1.  既存のプロシージャをスタートアップ プロシージャとして指定する。  
  
    2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタートアップ時にプロシージャが実行されないようにする。  
  
###  <a name="Security"></a> セキュリティ  
 詳細については、「[EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)」および「[EXECUTE AS 句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)」を参照してください。  
  
####  <a name="Permissions"></a> Permissions  
 詳細については、「 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)でストアド プロシージャを実行する方法について説明します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-execute-a-stored-procedure"></a>ストアド プロシージャを実行するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続して、そのインスタンスを展開します。次に、 **[データベース]** を展開します。  
  
2.  目的のデータベースを展開し、 **[プログラミング]** を展開します。次に、 **[ストアド プロシージャ]** を展開します。  
  
3.  目的のユーザー定義のストアド プロシージャを右クリックし、 **[ストアド プロシージャの実行]** をクリックします。  
  
4.  **[プロシージャの実行]** ダイアログ ボックスで、各パラメーターの値と、null 値を渡すかどうかを指定します。  
  
     **パラメーター**  
     パラメーターの名前を示します。  
  
     **[データ型]**  
     パラメーターのデータ型を示します。  
  
     **[出力パラメーター]**  
     これが出力パラメーターかどうかを示します。  
  
     **[NULL 値を渡す]**  
     パラメーターの値として NULL を渡します。  
  
     **Value**  
     プロシージャを呼び出すときのパラメーターの値を入力します。  
  
5.  ストアド プロシージャを実行するには、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-execute-a-stored-procedure"></a>ストアド プロシージャを実行するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例は、1 つのパラメーターを受け取るストアド プロシージャを実行する方法を示します。 この例では、 `uspGetEmployeeManagers` パラメーター値として値  `6` を指定して、 `@EmployeeID` ストアド プロシージャを実行します。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
#### <a name="to-set-or-clear-a-procedure-for-executing-automatically"></a>プロシージャの自動実行を設定または解除するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例は、 [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) を使用してプロシージャの自動実行を設定する方法を示しています。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';  
```  
  
#### <a name="to-stop-a-procedure-from-executing-automatically"></a>プロシージャの自動実行を解除するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例は、 [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) を使用して、プロシージャの自動実行を解除する方法を示しています。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';  
```  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
  
## <a name="see-also"></a>参照  
 [パラメーターの指定](../../relational-databases/stored-procedures/specify-parameters.md)   
 [scan for startup procs サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [ストアド プロシージャ &#40;データベース エンジン&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  
