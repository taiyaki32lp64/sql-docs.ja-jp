---
title: ユーザー定義関数の表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.udfproperties.general.f1
- sql13.swb.functionproperties.general.f1
helpviewer_keywords:
- displaying user-defined functions
- viewing user-defined functions
- user-defined functions [SQL Server], viewing
- status information [SQL Server], user-defined functions
ms.assetid: a45dfab5-6384-4311-b935-2e23a70c5c10
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 076fd5f22fb7df7801ce0dacb08126a55a735d40
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72905517"
---
# <a name="view-user-defined-functions"></a>ユーザー定義関数の表示
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のユーザー定義関数の定義またはプロパティに関する情報は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して取得できます。 関数のデータが元のテーブルからどのように抽出されているのかを理解したり、関数で定義されているデータを確認するために、関数の定義を調べたい場合があります。  
  
> [!IMPORTANT]  
>  関数から参照しているオブジェクトの名前を変更する場合は、関数のテキストに新しいオブジェクト名が反映されるように関数を変更する必要があります。 したがって、オブジェクトの名前を変更する前に、まずオブジェクトの依存関係を表示して、オブジェクト名の変更により影響を受ける関数があるかどうかを確認してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **関数に関する情報を取得するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sys.sql_expression_dependencies** を使用して関数のすべての依存関係を検索するには、データベースに対する VIEW DEFINITION 権限とデータベースの **sys.sql_expression_dependencies** に対する SELECT 権限が必要です。 OBJECT_DEFINITION で返されるようなシステム オブジェクトの定義は公開されます。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-show-a-user-defined-functions-properties"></a>ユーザー定義関数のプロパティを表示するには  
  
1.  **オブジェクト エクスプローラー**で、プロパティを表示する関数を含むデータベースの横にあるプラス記号をクリックします。次に、プラス記号をクリックして **[プログラミング]** フォルダーを展開します。  
  
2.  プラス記号をクリックして **[関数]** フォルダーを展開します。  
  
3.  プロパティを表示する関数を含むフォルダーをプラス記号をクリックして展開します。  
  
    -   Table-valued Function  
  
    -   スカラー値関数  
  
    -   集計関数  
  
4.  プロパティを表示する関数を右クリックし、 **[プロパティ]** を選択します。  

     **[関数のプロパティ - _function_name_]** ダイアログ ボックスに、次のプロパティが表示されます。  
  
     **[データベース]**  
     この関数を含むデータベースの名前です。  
  
     **[サーバー]**  
     現在のサーバー インスタンスの名前です。  
  
     **ユーザー**  
     この接続のユーザーの名前です。  
  
     **[作成日]**  
     関数が作成された日付を表示します。  
  
     **[実行時の権限]**  
     関数の実行コンテキストです。  
  
     **[名前]**  
     現在の関数の名前です。  
  
     **[スキーマ]**  
     関数を所有するスキーマを表示します。  
  
     **[システム オブジェクト]**  
     関数がシステム オブジェクトかどうかを指定します。 値は True と False です。  
  
     **[ANSI NULL]**  
     オブジェクトが ANSI NULL オプションで作成されたかどうかを指定します。  
  
     **Encrypted**  
     関数が暗号化されているかどうかを指定します。 値は True と False です。  
  
     **[関数の種類]**  
     ユーザー定義関数の種類です。  
  
     **[引用符で囲まれた識別子]**  
     オブジェクトが引用符で囲まれた識別子オプションで作成されたかどうかを指定します。  
  
     **[スキーマ バインド]**  
     関数がスキーマ バインドされているかどうかを指定します。 値は True と False です。 スキーマ バインド関数の詳細については、「[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)」の SCHEMABINDING のセクションを参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-get-the-definition-and-properties-of-a-function"></a>関数の定義およびプロパティを取得するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次のいずれかの例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the function name, definition, and relevant properties  
    SELECT sm.object_id,   
       OBJECT_NAME(sm.object_id) AS object_name,   
       o.type,   
       o.type_desc,   
       sm.definition,  
       sm.uses_ansi_nulls,  
       sm.uses_quoted_identifier,  
       sm.is_schema_bound,  
       sm.execute_as_principal_id  
    -- using the two system tables sys.sql_modules and sys.objects  
    FROM sys.sql_modules AS sm  
    JOIN sys.objects AS o ON sm.object_id = o.object_id  
    -- from the function 'dbo.ufnGetProductDealerPrice'  
    WHERE sm.object_id = OBJECT_ID('dbo.ufnGetProductDealerPrice')  
    ORDER BY o.type;  
    GO  
  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the definition of the function dbo.ufnGetProductDealerPrice  
    SELECT OBJECT_DEFINITION (OBJECT_ID('dbo.ufnGetProductDealerPrice')) AS ObjectDefinition;  
    GO  
    ```  
  
 詳細については、「[sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)」および「[OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)」を参照してください。  
  
#### <a name="to-get-the-dependencies-of-a-function"></a>関数の依存関係を取得するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get all of the dependency information  
    SELECT OBJECT_NAME(sed.referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(sed.referencing_id, sed.referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        sed.referencing_class_desc, sed.referenced_class_desc,  
        sed.referenced_server_name, sed.referenced_database_name, sed.referenced_schema_name,  
        sed.referenced_entity_name,   
        COALESCE(COL_NAME(sed.referenced_id, sed.referenced_minor_id), '(n/a)') AS referenced_column_name,  
        sed.is_caller_dependent, sed.is_ambiguous  
    -- from the two system tables sys.sql_expression_dependencies and sys.object  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    -- on the function dbo.ufnGetProductDealerPrice  
    WHERE sed.referencing_id = OBJECT_ID('dbo.ufnGetProductDealerPrice');  
    GO  
    ```  
  
 詳細については、「[sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)」および「[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。  
  
  
