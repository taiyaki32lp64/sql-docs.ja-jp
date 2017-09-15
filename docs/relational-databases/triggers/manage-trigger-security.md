---
title: "トリガーのセキュリティの管理 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d86813b142cbd85527fb1e4e1c11d87884258ecf
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="manage-trigger-security"></a>トリガーのセキュリティの管理
  既定では、DML トリガーも DDL トリガーも、トリガーを呼び出したユーザーのコンテキストで実行されます。 トリガーの呼び出し元は、トリガーが実行される原因となったステートメントを実行したユーザーです。 たとえば、ユーザー **Mary** が DELETE ステートメントを実行し、このために DML トリガー **DML_trigMary** が実行された場合、 **DML_trigMary** 内のコードは、 **Mary**のユーザー権限のコンテキストで実行されます。 この既定の動作は、悪意のあるコードをデータベースやサーバー インスタンスに組み込もうとするユーザーによって悪用される危険性があります。 たとえば、次の DDL トリガーがユーザー `JohnDoe`により作成されたとします。  
  
 `CREATE TRIGGER DDL_trigJohnDoe`  
  
 `ON DATABASE`  
  
 `FOR ALTER_TABLE`  
  
 `AS`  
  
 `GRANT CONTROL SERVER TO JohnDoe ;`  
  
 `GO`  
  
 このトリガーの内容は、 `GRANT CONTROL SERVER` sysadmin **固定サーバー ロールのメンバーなど、** ステートメントを実行する権限を持ったユーザーが `ALTER TABLE` ステートメントを実行した直後に、 `JohnDoe` に `CONTROL SERVER` 権限を付与するようにしています。 つまり、 `JohnDoe` 自身は `CONTROL SERVER` 権限を自分に付与することはできませんが、トリガー コードを利用して、上位の特権の下での実行権限を獲得しています。 DML トリガーも DDL トリガーも、このようなセキュリティの脅威にさらされています。  
  
## <a name="trigger-security-best-practices"></a>トリガーのセキュリティに関するベスト プラクティス  
 次の方法を使用することで、トリガー コードが上位の特権の下で実行されないようにすることができます。  
  
-   [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) カタログ ビューと [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md) カタログ ビューをクエリし、データベースとサーバー インスタンスに存在する DML トリガーおよび DDL トリガーを認識します。 次のクエリは、現在のデータベースにあるすべての DML とデータベースレベルのすべての DDL トリガーと、サーバー インスタンスにあるすべてのサーバー レベルの DDL トリガーを返します。  
  
    ```  
    SELECT type, name, parent_class_desc FROM sys.triggers  
    UNION  
    SELECT type, name, parent_class_desc FROM sys.server_triggers ;  
    ```  
  
-   [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) を使用して、トリガーが上位の特権の下で実行された場合に、データベースやサーバーの整合性に支障をきたす可能性のあるトリガーを無効にします。 次のステートメントは、現在のデータベースにあるすべてのデータベースレベルの DDL トリガーを無効にします。  
  
    ```  
    DISABLE TRIGGER ALL ON DATABASE  
    ```  
  
     このステートメントは、サーバー インスタンスにあるすべてのサーバーレベルの DDL トリガーを無効にします。  
  
    ```  
    DISABLE TRIGGER ALL ON ALL SERVER  
    ```  
  
     このステートメントは、現在のデータベースにあるすべての DML トリガーを無効にします。  
  
    ```  
    DECLARE @schema_name sysname, @trigger_name sysname, @object_name sysname ;  
    DECLARE @sql nvarchar(max) ;  
    DECLARE trig_cur CURSOR FORWARD_ONLY READ_ONLY FOR  
        SELECT SCHEMA_NAME(schema_id) AS schema_name,  
            name AS trigger_name,  
            OBJECT_NAME(parent_object_id) as object_name  
        FROM sys.objects WHERE type in ('TR', 'TA') ;  
  
    OPEN trig_cur ;  
    FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        SELECT @sql = 'DISABLE TRIGGER ' + QUOTENAME(@schema_name) + '.'  
            + QUOTENAME(@trigger_name) +  
            ' ON ' + QUOTENAME(@schema_name) + '.'   
            + QUOTENAME(@object_name) + ' ; ' ;  
        EXEC (@sql) ;  
        FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
    END  
    GO  
  
    -- Verify triggers are disabled. Should return an empty result set.  
    SELECT * FROM sys.triggers WHERE is_disabled = 0 ;  
    GO  
  
    CLOSE trig_cur ;  
    DEALLOCATE trig_cur;  
    ```  
  
## <a name="see-also"></a>参照  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DML トリガー](../../relational-databases/triggers/dml-triggers.md)   
 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)  
  
  