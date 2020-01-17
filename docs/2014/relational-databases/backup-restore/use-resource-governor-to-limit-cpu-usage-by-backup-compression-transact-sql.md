---
title: リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup compression [SQL Server], Resource Governor
- backup compression [SQL Server], CPU usage
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- Resource Governor, backup compression
ms.assetid: 01796551-578d-4425-9b9e-d87210f7ba72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fcd3d72ef3e716cd640d35505b82df459eb37b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920787"
---
# <a name="use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql"></a>リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 (Transact-SQL)
  既定の設定では、圧縮を使用してバックアップを行うと CPU 使用率が著しく増加し、圧縮処理に CPU が追加で消費されるために、同時に実行中の操作が悪影響を受ける可能性があります。 このため、CPU の競合が発生したときは、[リソース ガバナー](../resource-governor/resource-governor.md) によって CPU 使用率が制限されるセッションで、優先度の低い圧縮されたバックアップを作成することが必要になる場合もあります。 このトピックでは、このような場合に CPU 使用率を制限するリソース ガバナー ワークロード グループに、特定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーのセッションをマップしてそれらのセッションを分類するシナリオを示します。  
  
> [!IMPORTANT]  
>  所定のリソース ガバナーのシナリオでは、セッションの分類が、ユーザー名、アプリケーション名、または接続を区別できるその他の要素に基づいて行われます。 詳細については、「 [Resource Governor Classifier Function](../resource-governor/resource-governor-classifier-function.md) 」および「 [Resource Governor Workload Group](../resource-governor/resource-governor-workload-group.md)」を参照してください。  
  
##  <a name="Top"></a> このトピックでは、一連のシナリオを以下の順序で取り上げます。  
  
1.  [優先度の低い操作を行うためのログインとユーザーの設定](#setup_login_and_user)  
  
2.  [CPU 使用率を制限するためのリソース ガバナーの構成](#configure_RG)  
  
3.  [現在のセッションの分類の確認 (Transact-SQL)](#verifying)  
  
4.  [CPU が制限されているセッションを使用したバックアップの圧縮](#creating_compressed_backup)  
  
##  <a name="setup_login_and_user"></a> 優先度の低い操作を行うためのログインとユーザーの設定  
 このトピックのシナリオには、優先度の低い [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインおよびユーザーが必要です。 ユーザー名は、このログインで実行されるセッションを分類し、CPU 使用率を制限するリソース ガバナー ワークロード グループにセッションをルーティングするために使用されます。  
  
 以下では、この目的でログインとユーザーを設定する手順について説明した後に、[!INCLUDE[tsql](../../includes/tsql-md.md)] の例「例 A :ログインとユーザーの設定 (Transact-SQL)」を説明します。  
  
### <a name="to-set-up-a-login-and-database-user-for-classifying-sessions"></a>セッションを分類するためにログインとデータベース ユーザーを設定するには  
  
1.  優先度の低い圧縮されたバックアップを作成するための [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを作成します。  
  
     **ログインを作成するには**  
  
    -   [ログインの作成](../security/authentication-access/create-a-login.md)  
  
    -   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
2.  必要に応じて、このログインに VIEW SERVER STATE 権限を付与します。  
  
    -   [GRANT (システム オブジェクトの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-system-object-permissions-transact-sql)  
  
     詳細については、「[GRANT (データベース プリンシパルの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-principal-permissions-transact-sql)」を参照してください。  
  
3.  このログインに対して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーを作成します。  
  
     **ユーザーを作成するには**  
  
    -   [データベース ユーザーの作成](../security/authentication-access/create-a-database-user.md)  
  
    -   [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
4.  このログインおよびユーザーのセッションで特定のデータベースをバックアップできるようにするには、対象となるデータベースの db_backupoperator データベース ロールにこのユーザーを追加します。 この作業は、このユーザーがバックアップするデータベースごとに行います。 必要に応じて、このユーザーを他の固定データベース ロールに追加します。  
  
     **固定データベース ロールにユーザーを追加するには**  
  
    -   [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)  
  
     詳細については、「[GRANT (データベース プリンシパルの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-principal-permissions-transact-sql)」を参照してください。  
  
### <a name="example-a-setting-up-a-login-and-user-transact-sql"></a>例 a:ログインとユーザーの設定 (Transact-SQL)  
 次の例は、優先度の低いバックアップ用に新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインおよびユーザーを作成する場合にのみ該当します。 既存のログインとユーザーで適切なものがあれば、それを使用してもかまいません。  
  
> [!IMPORTANT]  
>  次の例では、サンプルのログインとユーザー名 *domain_name*`\MAX_CPU`を使用しています。 この名前を、優先度の低い圧縮されたバックアップを作成する際に使用する予定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインおよびユーザーの名前に置き換えてください。  
  
 この例では、Windows アカウント *domain_name*`\MAX_CPU` にログインを作成し、このログインに VIEW SERVER STATE 権限を付与します。 この権限によって、リソース ガバナーでログインのセッションがどのように分類されるかを確認できます。 次にこの例では、 *domain_name*`\MAX_CPU` のユーザーを作成し、このユーザーを [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] サンプル データベースの db_backupoperator 固定データベース ロールに追加します。 このユーザー名は、リソース ガバナーの分類子関数で使用されます。  
  
```sql  
-- Create a SQL Server login for low-priority operations  
USE master;  
CREATE LOGIN [domain_name\MAX_CPU] FROM WINDOWS;  
GRANT VIEW SERVER STATE TO [domain_name\MAX_CPU];  
GO  
-- Create a SQL Server user in AdventureWorks2012 for this login  
USE AdventureWorks2012;  
CREATE USER [domain_name\MAX_CPU] FOR LOGIN [domain_name\MAX_CPU];  
EXEC sp_addrolemember 'db_backupoperator', 'domain_name\MAX_CPU';  
GO  
  
```  
  
 [&#91;先頭に戻る&#93;](#Top)  
  
##  <a name="configure_RG"></a> CPU 使用率を制限するためのリソース ガバナーの構成  
  
> [!NOTE]  
>  リソース ガバナーが有効になっていることを確認してください。 詳細については、「 [リソース ガバナーの有効化](../resource-governor/enable-resource-governor.md)」を参照してください。  
  
 このリソース ガバナーのシナリオでは、次の基本的な手順で構成が行われます。  
  
1.  リソース ガバナーのリソース プールを作成し、CPU の競合が発生したときにリソース プール内の要求に割り当てられる最大平均 CPU 帯域幅を制限するように構成します。  
  
2.  このプールを使用するリソース ガバナー ワークロード グループを作成して構成します。  
  
3.  ユーザー定義関数 (UDF) である *分類子関数*を作成します。リソース ガバナーは、この関数の戻り値を使用してセッションを分類し、適切なワークロード グループにセッションがルーティングされるようにします。  
  
4.  分類子関数をリソース ガバナーに登録します。  
  
5.  リソース ガバナーのメモリ内の構成に変更を適用します。  
  
> [!NOTE]  
>  リソース ガバナーのリソース プール、ワークロード グループ、および分類の詳細については、「 [リソース ガバナー](../resource-governor/resource-governor.md)」をご覧ください。  
  
 上記の手順で使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントについては、「CPU 使用率を制限するようにリソース ガバナーを構成するには」で説明し、その後に [!INCLUDE[tsql](../../includes/tsql-md.md)] の例を示します。  
  
 **リソース ガバナーを構成するには (SQL Server Management Studio)**  
  
-   [テンプレートを使用してリソース ガバナーを構成する](../resource-governor/configure-resource-governor-using-a-template.md)  
  
-   [リソース プールの作成](../resource-governor/create-a-resource-pool.md)  
  
-   [ワークロード グループの作成](../resource-governor/create-a-workload-group.md)  
  
### <a name="to-configure-resource-governor-for-limiting-cpu-usage-transact-sql"></a>CPU 使用率を制限するようにリソース ガバナーを構成するには (Transact-SQL)  
  
1.  [CREATE RESOURCE POOL](/sql/t-sql/statements/create-resource-pool-transact-sql) ステートメントを実行してリソース プールを作成します。 この手順の例では、次の構文を使用します。  
  
     *CREATE RESOURCE POOL pool_name* WITH ( MAX_CPU_PERCENT = *value* );  
  
     *Value* は、最大平均 CPU 帯域幅の割合を示す 1 ～ 100 の整数です。 適切な値は環境によって異なります。 わかりやすいように、このトピックの例では 20% (MAX_CPU_PERCENT = 20) を使用します。  
  
2.  [CREATE WORKLOAD GROUP](/sql/t-sql/statements/create-workload-group-transact-sql) ステートメントを実行して、CPU 使用率を制限する優先度の低い操作用にワークロード グループを作成します。 この手順の例では、次の構文を使用します。  
  
     CREATE WORKLOAD GROUP *group_name* USING *pool_name*;  
  
3.  [CREATE FUNCTION](/sql/t-sql/statements/create-function-transact-sql) ステートメントを実行して、前の手順で作成したワークロード グループを優先度の低いログインのユーザーにマップする分類子関数を作成します。 この手順の例では、次の構文を使用します。  
  
     CREATE FUNCTION [*schema_name*.]*function_name*() RETURNS sysname  
  
     WITH SCHEMABINDING  
  
     AS  
  
     BEGIN  
  
     DECLARE @workload_group_name AS *sysname*  
  
     IF (SUSER_NAME() = '*user_of_low_priority_login*')  
  
     SET @workload_group_name = '*workload_group_name*'  
  
     RETURN @workload_group_name  
  
     END  
  
     この CREATE FUNCTION ステートメントのコンポーネントの詳細については、次のトピックを参照してください。  
  
    -   [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
    -   [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql)  
  
        > [!IMPORTANT]  
        >  SUSER_NAME は、分類子関数で使用できるシステム関数の 1 つです。 詳細については、「 [ユーザー定義の分類子関数の作成とテスト](../resource-governor/create-and-test-a-classifier-user-defined-function.md)」を参照してください。  
  
    -   [SET @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/set-local-variable-transact-sql).  
  
4.  [ALTER RESOURCE GOVERNOR](/sql/t-sql/statements/alter-resource-governor-transact-sql) ステートメントを実行して、分類子関数をリソース ガバナーに登録します。 この手順の例では、次の構文を使用します。  
  
     ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = *schema_name*.*function_name*);  
  
5.  次のように 2 回目の ALTER RESOURCE GOVERNOR ステートメントを実行して、リソース ガバナーのメモリ内の構成に変更を適用します。  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    ```  
  
### <a name="example-b-configuring-resource-governor-transact-sql"></a>例 b:Resource Governor の構成 (Transact-SQL)  
 次の例では、以下の手順を 1 つのトランザクションで実行します。  
  
1.  `pMAX_CPU_PERCENT_20` リソース プールを作成します。  
  
2.  `gMAX_CPU_PERCENT_20` ワークロード グループを作成します。  
  
3.  前の例で作成したユーザー名を使用する `rgclassifier_MAX_CPU()` 分類子関数を作成します。  
  
4.  分類子関数をリソース ガバナーに登録します。  
  
 この例では、トランザクションをコミットした後に、ALTER WORKLOAD GROUP または ALTER RESOURCE POOL ステートメントで要求された構成の変更が適用されます。  
  
> [!IMPORTANT]  
>  次の例では、「例 A: ログインとユーザーの設定 (Transact-SQL)」で作成したサンプルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーのユーザー名*domain_name*`\MAX_CPU` を使用しています。 この名前を、優先度の低い圧縮されたバックアップを作成する際に使用する予定のログインのユーザーの名前に置き換えてください。  
  
```sql  
-- Configure Resource Governor.  
BEGIN TRAN  
USE master;  
-- Create a resource pool that sets the MAX_CPU_PERCENT to 20%.   
CREATE RESOURCE POOL pMAX_CPU_PERCENT_20  
   WITH  
      (MAX_CPU_PERCENT = 20);  
GO  
-- Create a workload group to use this pool.   
CREATE WORKLOAD GROUP gMAX_CPU_PERCENT_20  
USING pMAX_CPU_PERCENT_20;  
GO  
-- Create a classification function.  
-- Note that any request that does not get classified goes into   
-- the 'Default' group.  
CREATE FUNCTION dbo.rgclassifier_MAX_CPU() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
    DECLARE @workload_group_name AS sysname  
      IF (SUSER_NAME() = 'domain_name\MAX_CPU')  
          SET @workload_group_name = 'gMAX_CPU_PERCENT_20'  
    RETURN @workload_group_name  
END;  
GO  
  
-- Register the classifier function with Resource Governor.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION= dbo.rgclassifier_MAX_CPU);  
COMMIT TRAN;  
GO  
-- Start Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
 [&#91;先頭に戻る&#93;](#Top)  
  
##  <a name="verifying"></a> 現在のセッションの分類の確認 (Transact-SQL)  
 必要に応じて、分類子関数で指定したユーザーとしてログインし、オブジェクト エクスプローラーで次の [SELECT](/sql/t-sql/queries/select-transact-sql) ステートメントを実行してセッションの分類を確認します。  
  
```sql  
USE master;  
SELECT sess.session_id, sess.login_name, sess.group_id, grps.name   
FROM sys.dm_exec_sessions AS sess   
JOIN sys.dm_resource_governor_workload_groups AS grps   
    ON sess.group_id = grps.group_id  
WHERE session_id > 50;  
GO  
```  
  
 結果ペインの **[名前]** 列に、分類子関数で指定したワークロード グループ名のセッションが 1 つ以上表示されるはずです。  
  
> [!NOTE]  
>  この SELECT ステートメントで呼び出される動的管理ビューの詳細については、「[sys.dm_exec_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql)」および「[sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql)」をご覧ください。  
  
 [&#91;先頭に戻る&#93;](#Top)  
  
##  <a name="creating_compressed_backup"></a> CPU が制限されているセッションを使用したバックアップの圧縮  
 最大 CPU が制限されているセッションで圧縮されたバックアップを作成するには、分類子関数で指定したユーザーでログインします。 バックアップ コマンドで、WITH COMPRESSION ([!INCLUDE[tsql](../../includes/tsql-md.md)]) を指定するか、 **[バックアップを圧縮する]** ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) を選択します。 圧縮されたデータベース バックアップを作成する方法については、「[データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)」をご覧ください。  
  
### <a name="example-c-creating-a-compressed-backup-transact-sql"></a>例 c:圧縮されたバックアップの作成 (Transact-SQL)  
 次に示す [BACKUP](/sql/t-sql/statements/backup-transact-sql) の例では、 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースの圧縮された完全バックアップを、新たな形式のバックアップ ファイル `Z:\SQLServerBackups\AdvWorksData.bak`に作成します。  
  
```sql  
--Run backup statement in the gBackup session.  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   MEDIADESCRIPTION='AdventureWorks2012 Compressed Data Backups'  
   DESCRIPTION='First database backup on AdventureWorks2012 Compressed Data Backups media set'  
   COMPRESSION;  
GO  
```  
  
 [&#91;先頭に戻る&#93;](#Top)  
  
## <a name="see-also"></a>参照  
 [ユーザー定義の分類子関数の作成とテスト](../resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [リソース ガバナー](../resource-governor/resource-governor.md)  
  
  
