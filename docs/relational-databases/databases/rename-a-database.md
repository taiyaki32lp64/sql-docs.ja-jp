---
title: データベースの名前変更 | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a2cfe01b4df32e0966084866a67cea4bfd57bc11
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907428"
---
# <a name="rename-a-database"></a>データベースの名前変更

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または Azure SQL Database で、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、ユーザー定義のデータベースの名前を変更する方法について説明します。 識別子の規則に従っていれば、データベースの名前にはいずれの文字も使用できます。  
  
## <a name="in-this-topic"></a>このトピックの内容
  
- 作業を開始する準備:  
  
     [制限事項と制約事項](#limitations-and-restrictions)  
  
     [セキュリティ](#security)  
  
- 以下を使用してデータベースの名前を変更するには:  
  
     [SQL Server Management Studio](#rename-a-database-using-sql-server-management-studio)  
  
     [Transact-SQL](#rename-a-database-using-transact-sql)  
  
- **補足情報:** [データベースの名前を変更した後](#backup-after-renaming-a-database)  

> [!NOTE]
> Azure SQL Data Warehouse または Parallel Data Warehouse でデータベースの名前を変更するには、[RENAME (Transact-SQL)](../../t-sql/statements/rename-transact-sql.md) ステートメントを使用します。
  
## <a name="before-you-begin"></a>はじめに
  
### <a name="limitations-and-restrictions"></a>制限事項と制約事項  
  
- システム データベースの名前は変更できません。
- 他のユーザーがデータベースにアクセスしている間は、データベースの名前を変更することはできません。 
  - SQL Server では、データベースをシングル ユーザー モードに設定することで、開いているすべての接続を閉じることができます。 詳細については、「 [データベースをシングル ユーザー モードに設定する](../../relational-databases/databases/set-a-database-to-single-user-mode.md)」を参照してください。
  - Azure SQL Database では、名前を変更するデータベースに対して他のユーザーが接続を開いていないことを確認する必要があります。
  
### <a name="security"></a>Security  
  
#### <a name="permissions"></a>アクセス許可

データベースに対する ALTER 権限が必要です。  
  
## <a name="rename-a-database-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してデータベースの名前を変更する

SQL Server Management Studio を使用して SQL Server または Azure SQL データベースの名前を変更するには、次の手順を使用します。

  
1. **オブジェクト エクスプローラー**で、SQL インスタンスに接続します。  
  
2. データベースに対して開いている接続がないことを確認します。 SQL Server を使用している場合は、[データベースをシングル ユーザー モードに設定する](../../relational-databases/databases/set-a-database-to-single-user-mode.md)ことで、開いているすべての接続を閉じ、データベース名の変更中は他のユーザーが接続できないようにすることができます。  
  
3. オブジェクト エクスプローラーで **[データベース]** を展開し、名前を変更するデータベースを右クリックし、 **[名前の変更]** をクリックします。  
  
4. 新しいデータベース名を入力し、 **[OK]** をクリックします。  
  
5. 任意で、データベースがご利用の既定のデータベースであった場合、「[名称変更後、既定のデータベースを再設定する](#reset-your-default-database-after-rename)」を参照してください。

## <a name="rename-a-database-using-transact-sql"></a>Transact-SQL を使用してデータベースの名前を変更する  
  
### <a name="to-rename-a-sql-server-database-by-placing-it-in-single-user-mode"></a>SQL Server データベースをシングル ユーザー モードにすることで名前を変更するには

SQL Server Management Studio で T-SQL を使用して SQL Server データベースの名前を変更するには、データベースをシングル ユーザー モードにして名前を変更した後、マルチモード ユーザーに戻す手順を含む次の手順を使用します。
  
1. インスタンスの `master` データベースに接続します。  
2. クエリ ウィンドウを開きます。  
3. 次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 `MyTestDatabase` データベースの名前を `MyTestDatabaseCopy`に変更します。
  
   ```sql
   USE master;  
   GO  
   ALTER DATABASE MyTestDatabase SET SINGLE_USER WITH ROLLBACK IMMEDIATE
   GO
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   GO  
   ALTER DATABASE MyTestDatabaseCopy SET MULTI_USER
   GO
   ```  

4. 任意で、データベースがご利用の既定のデータベースであった場合、「[名称変更後、既定のデータベースを再設定する](#reset-your-default-database-after-rename)」を参照してください。

### <a name="to-rename-an-azure-sql-database-database"></a>Azure SQL Database データベースの名前を変更するには

SQL Server Management Studio で T-SQL を使用して Azure SQL データベースの名前を変更するには、次の手順を使用します。
  
1. インスタンスの `master` データベースに接続します。  
2. クエリ ウィンドウを開きます。
3. データベースが使用されていないことを確認します。
4. 次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 `MyTestDatabase` データベースの名前を `MyTestDatabaseCopy`に変更します。
  
   ```sql
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   ```  

## <a name="backup-after-renaming-a-database"></a>データベースの名前を変更した後のバックアップ  

SQL Server 内のデータベースの名前を変更した後、`master` データベースをバックアップします。 Azure SQL database では、バックアップは自動的に発生するため、この操作は必要ありません。  
  
## <a name="reset-your-default-database-after-rename"></a>名称変更後、既定のデータベースを再設定する

名前を変更するデータベースがご利用の既定のデータベースであった場合、次のコマンドを使用し、名前を変更したデータベースに既定を設定し直します。


```sql
USE [master]
GO
ALTER LOGIN [your-login] WITH DEFAULT_DATABASE=[new-database-name]
GO
```


## <a name="see-also"></a>参照

- [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)
- [データベース識別子](../../relational-databases/databases/database-identifiers.md)  
