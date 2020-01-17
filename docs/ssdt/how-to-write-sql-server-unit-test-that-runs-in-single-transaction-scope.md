---
title: 方法:単一のトランザクションのスコープ内で実行する SQL Server の単体テストを作成する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cb241e94-d81c-40e9-a7ae-127762a6b855
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8c1a9bf666ac79b76d94cfbd04c88bde6eafd85b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119879"
---
# <a name="how-to-write-a-sql-server-unit-test-that-runs-within-the-scope-of-a-single-transaction"></a>方法:単一のトランザクションのスコープ内で実行する SQL Server の単体テストを作成する
単体テストは、単一のトランザクションのスコープ内で実行されるように変更できます。 この方法を使用すると、テストの終了後、テストによって行われた変更をロールバックできます。 次の手順では、以下の操作方法について説明します。  
  
-   **BEGIN TRANSACTION** と **ROLLBACK TRANSACTION** を使用する Transact\-SQL テスト スクリプト内にトランザクションを作成します。  
  
-   テスト クラスで単一のテスト メソッドのトランザクションを作成します。  
  
-   指定したテスト クラスですべてのテスト メソッドのトランザクションを作成します。  
  
**前提条件**  
  
このトピックの一部の手順では、分散トランザクション コーディネーター サービスを、単体テストを実行するコンピューターで実行している必要があります。 詳しくは、このトピックの最後にある手順をご覧ください。  
  
## <a name="to-create-a-transaction-using-transact-sql"></a>Transact\-SQL を使用してトランザクションを作成するには  
  
#### <a name="to-create-a-transaction-using-transact-sql"></a>Transact\-SQL を使用してトランザクションを作成するには  
  
1.  SQL Server 単体テスト デザイナーで単体テストを開きます。 (デザイナーを表示するには、単体テストのソース コード ファイルをダブルクリックします)。  
  
2.  トランザクションを作成するスクリプトの種類を指定します。 たとえば、事前テスト、テスト、または事後テストを指定できます。  
  
3.  Transact\-SQL エディターで、テスト スクリプトを入力します。  
  
4.  次の簡単な例に示すように、`BEGIN TRANSACTION` ステートメントと `ROLLBACK TRANSACTION` ステートメントを挿入します。 この例では、50 行のデータが格納された OrderDetails という名前のデータベース テーブルを使用します。  
  
    ```  
    BEGIN TRANSACTION TestTransaction  
    UPDATE "OrderDetails" set Quantity = Quantity + 10  
    IF @@ROWCOUNT!=50  
    RAISERROR('Row count does not equal 50',16,1)  
    ROLLBACK TRANSACTION TestTransaction  
    ```  
  
    > [!NOTE]  
    > COMMIT TRANSACTION ステートメントの実行後にトランザクションをロールバックすることはできません。  
  
    ROLLBACK TRANSACTION がストアド プロシージャおよびトリガーとどのように連携するかについて詳しくは、Microsoft Web サイトの「[ROLLBACK TRANSACTION (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkID=115927)」をご覧ください。  
  
## <a name="to-create-a-transaction-for-a-single-test-method"></a>単一のテスト メソッドのトランザクションを作成するには  
この例では、[System.Transactions.TransactionScope](https://docs.microsoft.com/dotnet/api/system.transactions.transactionscope) 型を使用するときにアンビエント トランザクションを使用します。 既定では、実行接続および特権接続ではアンビエント トランザクションが使用されません。これらの接続は、メソッドが実行される前に作成されるためです。 SqlConnection には、トランザクションにアクティブな接続を関連付ける [System.Data.SqlClient.SqlConnection.EnlistTransaction](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlconnection.enlisttransaction) メソッドがあります。 アンビエント トランザクションを作成すると、そのトランザクション自体が現在のトランザクションとして登録されるため、[System.Transactions.Transaction.Current](https://docs.microsoft.com/dotnet/api/system.transactions.transaction.current) プロパティを介してそのトランザクションにアクセスできます。 この例では、アンビエント トランザクションが破棄されると、トランザクションはロールバックされます。 単体テストの実行時に行われたすべての変更をコミットする場合は、[System.Transactions.TransactionScope.Complete](https://docs.microsoft.com/dotnet/api/system.transactions.transactionscope.complete) メソッドを呼び出す必要があります。  
  
#### <a name="to-create-a-transaction-for-a-single-test-method"></a>単一のテスト メソッドのトランザクションを作成するには  
  
1.  **ソリューション エクスプローラー**で、テスト プロジェクトの **[参照設定]** ノードを右クリックし、 **[参照の追加]** をクリックします。  
  
    **[参照の追加]** ダイアログ ボックスが表示されます。  
  
2.  **[.NET]** タブをクリックします。  
  
3.  アセンブリの一覧で、 **[System.Transactions]** をクリックし、 **[OK]** をクリックします。  
  
4.  単体テストの Visual Basic ファイルまたは C# ファイルを開きます。  
  
5.  次の Visual Basic のコード例に示すように、事前テスト、テスト、および事後テストのアクションをラップします。  
  
    ```  
    <TestMethod()> _  
    Public Sub dbo_InsertTable1Test()  
  
        Using ts as New System.Transactions.TransactionScope( System.Transactions.TransactionScopeOption.Required)  
            ExecutionContext.Connection.EnlistTransaction(Transaction.Current)  
            PrivilegedContext.Connection.EnlistTransaction(Transaction.Current)  
  
            Dim testActions As DatabaseTestActions = Me.dbo_InsertTable1TestData  
            'Execute the pre-test script  
            '  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.PretestAction) Is Nothing), "Executing pre-test script...")  
            Dim pretestResults() As ExecutionResult = TestService.Execute(Me.PrivilegedContext, Me.PrivilegedContext, testActions.PretestAction)  
            'Execute the test script  
  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.TestAction) Is Nothing), "Executing test script...")  
            Dim testResults() As ExecutionResult = TestService.Execute(ExecutionContext, Me.PrivilegedContext, testActions.TestAction)  
  
            'Execute the post-test script  
            '  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.PosttestAction) Is Nothing), "Executing post-test script...")  
            Dim posttestResults() As ExecutionResult = TestService.Execute(Me.PrivilegedContext, Me.PrivilegedContext, testActions.PosttestAction)  
  
            'Because the transaction is not explicitly committed, it  
            'is rolled back when the ambient transaction is   
            'disposed.  
            'To commit the transaction, remove the comment delimiter  
            'from the following statement:  
            'ts.Complete()  
  
    End Sub  
    Private dbo_InsertTable1TestData As DatabaseTestActions  
    ```  
  
    > [!NOTE]  
    > Visual Basic を使用している場合は、(`Imports Microsoft.VisualStudio.TestTools.UnitTesting`、`Imports Microsoft.VisualStudio.TeamSystem.Data.UnitTesting`、および `Imports Microsoft.VisualStudio.TeamSystem.Data.UnitTest.Conditions` に加えて) `Imports System.Transactions` を追加する必要があります。Visual C# を使用している場合は、(Microsoft.VisualStudio.TestTools、Microsoft.VisualStudio.TeamSystem.Data.UnitTesting、および Microsoft.VisualStudio.TeamSystem.Data.UnitTesting.Conditions の `using` ステートメントに加えて) `using System.Transactions` を追加する必要があります。 また、プロジェクトへの参照をこれらのアセンブリに追加する必要もあります。  
  
## <a name="to-create-a-transaction-for-all-test-methods-in-a-test-class"></a>テスト クラスですべてのテスト メソッドのトランザクションを作成するには  
  
#### <a name="to-create-a-transaction-for-all-test-methods-in-a-test-class"></a>テスト クラスですべてのテスト メソッドのトランザクションを作成するには  
  
1.  単体テストの Visual Basic ファイルまたは C# ファイルを開きます。  
  
2.  次の Visual C# のコード例に示すように、TestInitialize でトランザクションを作成し、TestCleanup でそのトランザクションを破棄します。  
  
    ```  
    TransactionScope _trans;  
  
            [TestInitialize()]  
            public void Init()  
            {  
                _trans = new TransactionScope();  
                base.InitializeTest();  
            }  
  
            [TestCleanup()]  
            public void Cleanup()  
            {  
                base.CleanupTest();  
                _trans.Dispose();  
            }  
  
            [TestMethod()]  
            public void TransactedTest()  
            {  
                DatabaseTestActions testActions = this.DatabaseTestMethod1Data;  
                // Execute the pre-test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.PretestAction != null), "Executing pre-test script...");  
                ExecutionResult[] pretestResults = TestService.Execute(this.PrivilegedContext, this.PrivilegedContext, testActions.PretestAction);  
                // Execute the test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.TestAction != null), "Executing test script...");  
                ExecutionResult[] testResults = TestService.Execute(this.ExecutionContext, this.PrivilegedContext, testActions.TestAction);  
                // Execute the post-test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.PosttestAction != null), "Executing post-test script...");  
                ExecutionResult[] posttestResults = TestService.Execute(this.PrivilegedContext, this.PrivilegedContext, testActions.PosttestAction);  
  
            }  
    ```  
  
## <a name="to-start-the-distributed-transaction-coordinator-service"></a>分散トランザクション コーディネーター サービスを開始するには  
このトピックの一部の手順では、System.Transactions アセンブリ内の型を使用します。 これらの手順を実行する前に、単体テストを実行するコンピューターで、分散トランザクション コーディネーター サービスが実行されていることを確認する必要があります。 そうでない場合は、テストが失敗し、次のエラー メッセージが表示されます。"テスト メソッド *ProjectName*.*TestName*.*MethodName* が例外をスローしました:System.Data.SqlClient.SqlException: サーバー '*ComputerName*' の MSDTC は使用できません"。  
  
#### <a name="to-start-the-distributed-transaction-coordinator-service"></a>分散トランザクション コーディネーター サービスを開始するには  
  
1.  **コントロール パネル**を開きます。  
  
2.  **コントロール パネル**の **[管理ツール]** を開きます。  
  
3.  **[管理ツール]** の **[サービス]** を開きます。  
  
4.  **[サービス]** ウィンドウで、 **[分散トランザクション コントローラー]** サービスを右クリックし、 **[開始]** をクリックします。  
  
    サービスの状態が **[開始]** に更新されます。 これで、System.Transactions を使用する単体テストを実行できるようになります。  
  
> [!IMPORTANT]  
> 分散トランザクション コントローラー サービスを開始した場合でも、"`System.Transactions.TransactionManagerCommunicationException: Network access for Distributed Transaction Manager (MSDTC) has been disabled. Please enable DTC for network access in the security configuration for MSDTC using the Component Services Administrative tool. ---> System.Runtime.InteropServices.COMException: The transaction manager has disabled its support for remote/network transactions. (Exception from HRESULT: 0x8004D024)`" というエラーが表示されることがあります。 このエラーが表示される場合は、ネットワーク アクセス用に分散トランザクション コントローラーを構成する必要があります。 詳しくは、「[ネットワーク DTC アクセスを有効にする](https://go.microsoft.com/fwlink/?LinkId=193916)」をご覧ください。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
