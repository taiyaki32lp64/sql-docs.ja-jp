---
title: 部分的包含データベースへの移行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database, migrating to
ms.assetid: 90faac38-f79e-496d-b589-e8b2fe01c562
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e535935da5c99668e39ab4f84eb98ccd5bab064
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871731"
---
# <a name="migrate-to-a-partially-contained-database"></a>Migrate to a Partially Contained Database
  このトピックでは、部分的包含データベース モデルへの変更を準備する方法を説明し、移行手順を示します。  
  
 **このトピックの内容:**  
  
-   [データベースを移行する準備](#prepare)  
  
-   [包含データベースの有効化](#enable)  
  
-   [部分的包含へのデータベースの変換](#convert)  
  
-   [包含データベース ユーザーへのユーザーの移行](#users)  
  
##  <a name="prepare"></a> データベースを移行する準備  
 データベースを部分的包含データベース モデルに移行することを検討している場合は、次の点を確認してください。  
  
-   部分的包含データベース モデルを理解している。 詳細については、「 [包含データベース](contained-databases.md)」を参照してください。  
  
-   部分的包含データベースに固有のリスクを理解している。 詳細については、「 [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md)」を参照してください。  
  
-   包含データベースは、レプリケーション、変更データ キャプチャ、または変更の追跡をサポートしていない。 データベースがこれらの機能を使用していないことを確認してください。  
  
-   部分的包含データベースに関して変更されているデータベース機能の一覧を確認する。 詳細については、「[変更された機能 &#40;包含データベース&#41;](modified-features-contained-database.md)」を参照してください。  
  
-   [sys.dm_db_uncontained_entitiess &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql) クエリを実行し、データベース内の非包含オブジェクトまたは機能を検索します。 詳細については、以下を参照してください。  
  
-   **database_uncontained_usage** XEvent を監視し、非包含機能がいつ使用されるかを確認する。  
  
##  <a name="enable"></a> 包含データベースの有効化  
 包含データベースを作成するためには、あらかじめ [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスで包含データベースを有効にしておく必要があります。  
  
### <a name="enabling-contained-databases-using-transact-sql"></a>Transact SQL を使用して包含データベースを有効にする  
 次の例では、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスで包含データベースを有効にします。  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE ;  
GO  
```  
  
#### <a name="enabling-contained-databases-using-management-studio"></a>Management Studio を使用して包含データベースを有効にする  
 次の例では、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスで包含データベースを有効にします。  
  
1.  オブジェクト エクスプローラーでサーバー名を右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[詳細設定]** ページの **[包含]** セクションで、 **[包含データベースを有効にする]** オプションを **True**に設定します。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="convert"></a> 部分的包含へのデータベースの変換  
 データベースを包含データベースに変換するには、 **CONTAINMENT** オプションを変更します。  
  
### <a name="converting-a-database-to-partially-contained-using-transact-sql"></a>Transact-SQL を使用してデータベースを部分的包含に変換する  
 次の例では、 `Accounting` という名前のデータベースを部分的包含データベースに変換します。  
  
```sql  
USE [master]  
GO  
ALTER DATABASE [Accounting] SET CONTAINMENT = PARTIAL  
GO  
```  
  
### <a name="converting-a-database-to-partially-contained-using-management-studio"></a>Management Studio を使用してデータベースを部分的包含に変換する  
 次の例では、データベースを部分的包含データベースに変換します。  
  
1.  オブジェクト エクスプローラーで、 **[データベース]** を展開し、変換するデータベースを右クリックして、 **[プロパティ]** をクリックします。  
  
2.  **[オプション]** ページで、 **[包含の種類]** オプションを **[部分]** に変更します。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="users"></a> 包含データベース ユーザーへのユーザーの移行  
 次の例では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに基づくすべてのユーザーを、パスワードを持つ包含データベース ユーザーに移行します。 有効になっていないログインは除外します。 この例は、包含データベースで実行する必要があります。  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>参照  
 [包含データベース](contained-databases.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql)   
 [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql)  
  
  
