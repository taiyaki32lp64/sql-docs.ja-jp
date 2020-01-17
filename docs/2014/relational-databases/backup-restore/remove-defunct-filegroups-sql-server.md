---
title: 機能していないファイル グループの削除 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 2a59277110d91ffd40a2db7d62fd3a01aa109dfc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921554"
---
# <a name="remove-defunct-filegroups-sql-server"></a>機能していないファイル グループの削除 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、機能していないファイル グループを削除する方法を説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **機能していないファイル グループを削除する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   このトピックの内容は、複数のファイルまたはファイル グループを含む [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース (単純復旧モデルでは、読み取り専用ファイル グループのみ) に関するものです。  
  
-   オフラインのファイル グループが削除されると、ファイル グループ内のすべてのファイルが機能しなくなります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   ファイル グループが復元されておらず、復元する必要もなければ、データベースからそのファイル グループを削除することで、 *機能していない* 状態にすることができます。 機能していないファイル グループをこのデータベースに復元することはできませんが、そのメタデータはデータベース内に残ります。 ファイル グループが機能しなくなった後、データベースを再起動でき、復旧によって、復元されるファイル グループ間でデータベースの一貫性が維持されます。  
  
     たとえば、ファイル グループを機能していない状態にすることは、データベース内で不要になったオフライン ファイル グループによって生じた遅延トランザクションを解決する方法の 1 つです。 ファイル グループがオフラインであったことが原因で遅延されたトランザクションは、ファイル グループを機能していない状態にすると、遅延状態ではなくなります。 詳細については、「 [遅延トランザクション &#40;SQL Server&#41;](deferred-transactions-sql-server.md)を使用して、機能していないファイル グループを削除する方法を説明します。  
  
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
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 (**に注意してください。** この例では、ファイルとファイル グループが既に存在します。 これらのオブジェクトを作成するには、「[ALTER DATABASE の File および Filegroup オプション](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)」トピックの例 B を参照してください)。最初の例では、`test1dat3` ステートメントと `test1dat4` 句を使用して、`ALTER DATABASE` ファイルと `REMOVE FILE` ファイルを機能していないファイル グループから削除します。 2 番目の例では、`Test1FG1` 句を使用して、機能していないファイル グループ `REMOVE FILEGROUP` を削除します。  
  
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
  
## <a name="see-also"></a>関連項目  
 [ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [遅延トランザクション &#40;SQL Server&#41;](deferred-transactions-sql-server.md)   
 [ファイルの復元 &#40;完全復旧モデル&#41;](file-restores-full-recovery-model.md)   
 [ファイル復元 &#40;単純復旧モデル&#41;](file-restores-simple-recovery-model.md)   
 [Online Restore &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [ページ復元 &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
