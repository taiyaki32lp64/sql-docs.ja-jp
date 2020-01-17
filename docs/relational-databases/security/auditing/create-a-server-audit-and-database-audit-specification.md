---
title: サーバー監査およびデータベース監査の仕様を作成する
description: SQL Server Management Studio または Transact-SQL (T-SQL) を使用し、SQL Server の監査とデータベース監査の仕様を作成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d9ab1fa97653513d18c43b916ca5bfbc2105e8e7
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557877"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>サーバー監査の仕様およびデータベース監査の仕様を作成する方法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]でサーバー監査とデータベース監査の仕様を作成する方法について説明します。  
  
 *のインスタンスや* データベースの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、システムで発生するイベントの追跡およびログ記録が行われます。 *SQL Server Audit* オブジェクトは、監視するサーバー レベルまたはデータベース レベルのアクションおよびアクションのグループの 1 つのインスタンスを収集します。 監査は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス レベルで行われます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスごとに複数の監査を使用できます。 " *データベース レベルの監査の仕様* " オブジェクトも、監査に属しています。 各監査では、SQL Server データベースごとに 1 つのデータベース監査の仕様を作成できます。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **サーバー監査とデータベース監査の仕様を作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 データベース監査仕様は、セキュリティ保護できないオブジェクトであり、特定のデータベースに保存されます。 作成されたデータベース監査仕様は無効な状態です。  
  
 ユーザー データベースでデータベース監査の仕様を作成または変更するときは、システム ビューなど、サーバー スコープ オブジェクトの監査アクションは含めないでください。 サーバー スコープ オブジェクトが含まれている場合、監査が作成されます。 ただし、サーバー スコープ オブジェクトは対象にならず、エラーは返されません。 サーバー スコープ オブジェクトを監査するには、master データベースのデータベース監査の仕様を使用してください。  
  
 **tempdb** システム データベースを除き、データベース監査の仕様は、その仕様が作成されるデータベースに存在します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
  
-   ALTER ANY DATABASE AUDIT 権限を持つユーザーは、データベース監査仕様を作成し、任意の監査にバインドできます。  
  
-   データベース監査仕様の作成後は、CONTROL SERVER 権限または ALTER ANY DATABASE AUDIT 権限を持つプリンシパル、または sysadmin アカウントがその仕様を表示できます。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-server-audit"></a>サーバー監査を作成するには  
  
1.  オブジェクト エクスプローラーで、 **[セキュリティ]** フォルダーを展開します。  
  
2.  **[監査]** フォルダーを右クリックし、 **[新しい監査]** を選択します。詳しくは、「 [サーバー監査およびサーバー監査の仕様を作成する方法](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)」をご覧ください。  
  
3.  オプションの選択が完了したら、 **[OK]** をクリックします。  

#### <a name="to-create-a-database-level-audit-specification"></a>データベース レベルの監査仕様を作成するには  
  
1.  オブジェクト エクスプローラーで、監査仕様を作成するデータベースを展開します。  
  
2.  **[セキュリティ]** フォルダーを展開します。  
  
3.  **[データベース監査の仕様]** フォルダーを右クリックし、 **[新しいデータベース監査の仕様...]** を選択します。  
  
     **[データベース監査の仕様の作成]** ダイアログ ボックスでは、次のオプションを使用できます。  
  
     **Name**  
     データベース監査の仕様の名前。 この名前は、新しいサーバー監査の仕様を作成すると自動的に生成されますが、編集可能です。  
  
     **監査**  
     既存のサーバー監査オブジェクトの名前。 監査の名前を入力するか、一覧から選択します。  
  
     **[監査アクションの種類]**  
     キャプチャするデータベース レベルの監査アクション グループと監査アクションを指定します。 データベース レベルの監査アクション グループと監査アクションの一覧、およびそれらに含まれるイベントの説明については、「 [SQL Server 監査のアクション グループとアクション](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)」をご覧ください。  
  
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
  
4.  オプションの選択が完了したら、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-server-audit"></a>サーバー監査を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>データベース レベルの監査仕様を作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 `Audit_Pay_Tables` テーブルに対する `dbo` ユーザーによる SELECT ステートメントと INSERT ステートメントを、定義済みのサーバー監査に基づいて監査する `HumanResources.EmployeePayHistory` という名前のデータベース監査仕様を作成します。  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 詳細については、「[CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md)」と「[CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)」を参照してください。  
  
  
