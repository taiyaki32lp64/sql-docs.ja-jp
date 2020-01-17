---
title: 機能していないファイル グループの削除 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], defunct filegroups
- defunct filegroups
- restoring filegroups [SQL Server]
- deferred transactions
- filegroups [SQL Server], defunct
- unrestored filegroups
ms.assetid: 055f9c6a-5c18-4942-98e7-ec918f0ff975
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4314dbd1ab80fe8a26a1c6fa2b2429b68c6645fa
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908895"
---
# <a name="remove-defunct-filegroups-sql-server"></a>機能していないファイル グループの削除 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、機能していないファイル グループを削除する方法を説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **機能していないファイル グループを削除する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   このトピックの内容は、複数のファイルまたはファイル グループを含む [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース (単純復旧モデルでは、読み取り専用ファイル グループのみ) に関するものです。  
  
-   オフラインのファイル グループが削除されると、ファイル グループ内のすべてのファイルが機能しなくなります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   ファイル グループが復元されておらず、復元する必要もなければ、データベースからそのファイル グループを削除することで、 *機能していない* 状態にすることができます。 機能していないファイル グループをこのデータベースに復元することはできませんが、そのメタデータはデータベース内に残ります。 ファイル グループが機能しなくなった後、データベースを再起動でき、復旧によって、復元されるファイル グループ間でデータベースの一貫性が維持されます。  
  
     たとえば、ファイル グループを機能していない状態にすることは、データベース内で不要になったオフライン ファイル グループによって生じた遅延トランザクションを解決する方法の 1 つです。 ファイル グループがオフラインであったことが原因で遅延されたトランザクションは、ファイル グループを機能していない状態にすると、遅延状態ではなくなります。 詳細については、「 [遅延トランザクション &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)を使用して、機能していないファイル グループを削除する方法を説明します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-remove-defunct-filegroups"></a>機能していないファイル グループを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、ファイルを削除するデータベースを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[ファイル]** ページをクリックします。  
  
4.  **[データベース ファイル]** グリッドで、削除するファイルを選択し、 **[削除]** をクリックした後 **[OK]** をクリックします。  
  
5.  **[ファイル グループ]** ページをクリックします。  
  
6.  **[行]** グリッドで、削除するファイル グループを選択し、 **[削除]** をクリックした後 **[OK]** をクリックします。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-remove-defunct-filegroups"></a>機能していないファイル グループを削除するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 (**注:** この例では、ファイルとファイル グループが既に存在することを前提としています。 これらのオブジェクトを作成するには、「[ALTER DATABASE の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」トピックの例 B を参照してください)。最初の例では、`test1dat3` ステートメントと `test1dat4` 句を使用して、`ALTER DATABASE` ファイルと `REMOVE FILE` ファイルを機能していないファイル グループから削除します。 2 番目の例では、`Test1FG1` 句を使用して、機能していないファイル グループ `REMOVE FILEGROUP` を削除します。  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat3 ;  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4 ;  
GO  
  
```  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILEGROUP Test1FG1 ;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)   
 [遅延トランザクション &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)   
 [ファイルの復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [ファイル復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Online Restore &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
