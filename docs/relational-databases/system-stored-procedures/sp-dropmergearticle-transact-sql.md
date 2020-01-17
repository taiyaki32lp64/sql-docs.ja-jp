---
title: sp_dropmergearticle (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergearticle
- sp_dropmergearticle_TSQL
helpviewer_keywords:
- sp_dropmergearticle
ms.assetid: 5ef1fbf7-c03d-4488-9ab2-64aae296fa4f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 751f99cad3a2064dce366a90905918075cb697a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056481"
---
# <a name="spdropmergearticle-transact-sql"></a>sp_dropmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アーティクルをマージ パブリケーションから削除します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropmergearticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'   
    [ , [ @ignore_distributor= ] ignore_distributor   
    [ , [ @reserved= ] reserved   
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルを削除するパブリケーションの名前です。 *パブリケーション*は**sysname**、既定値はありません。  
  
`[ @article = ] 'article'` 指定したパブリケーションから削除するアーティクルの名前です。 *記事*は**sysname**、既定値はありません。 場合**すべて**、指定したマージ パブリケーションのすべての既存のアーティクルを削除します。 場合でも*記事*は**すべて**パブリケーションを削除しなければなりませんとは別に、アーティクルからです。  
  
`[ @ignore_distributor = ] ignore_distributor` ディストリビューターに接続しなくてもこのストアド プロシージャを実行するかどうかを示します。 *ignore_distributor*は**ビット**、既定値は**0**します。  
  
`[ @reserved = ] reserved` 将来使用するために予約されています。 *予約済み*は**nvarchar (20)** 、既定値は NULL です。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 有効またはスナップショットを無効にする機能を無効にします。 *更によって*は、**ビット**、既定値は、 **0**します。  
  
 **0**スナップショットが無効であることをマージ アーティクルへの変更が発生しないことを指定します。  
  
 **1**スナップショットが無効であることをマージ アーティクルへの変更が生じる場合、値があるかどうかと**1**新しいスナップショットを作成する権限が与えられます。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 確認、アーティクルを削除すると、既存のサブスクリプションの再初期化が必要があります。 *更によって*は、**ビット**、既定値は**0**します。  
  
 **0**アーティクルを削除するも、サブスクリプションを再初期化するのには発生しませんを指定します。  
  
 **1**記事により、再初期化するために既存のサブスクリプションを削除すると、サブスクリプションを再初期化が発生するの許可します。  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` 内部でのみ使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_dropmergearticle**はマージ レプリケーションで使用します。 アーティクルを削除する詳細については、次を参照してください。[記事を追加し、既存のパブリケーションからアーティクル](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)します。  
  
 実行**sp_dropmergearticle**パブリケーションからアーティクルを削除してから削除されません、オブジェクト、パブリケーション データベースまたはサブスクリプション データベースから対応するオブジェクト。 必要であれば `DROP <object>` を使用して、手動でこれらのオブジェクトを削除します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_dropmergearticle**します。  
  
## <a name="example"></a>例  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @table1 AS sysname;  
DECLARE @table2 AS sysname;  
DECLARE @table3 AS sysname;  
DECLARE @salesschema AS sysname;  
DECLARE @hrschema AS sysname;  
DECLARE @filterclause AS nvarchar(1000);  
SET @publication = N'AdvWorksSalesOrdersMerge';   
SET @table1 = N'Employee';   
SET @table2 = N'SalesOrderHeader';   
SET @table3 = N'SalesOrderDetail';   
SET @salesschema = N'Sales';  
SET @hrschema = N'HumanResources';  
SET @filterclause = N'Employee.LoginID = HOST_NAME()';  
  
-- Drop the merge join filter between SalesOrderHeader and SalesOrderDetail.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table3,   
  @filtername = N'SalesOrderDetail_SalesOrderHeader',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the merge join filter between Employee and SalesOrderHeader.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table2,   
  @filtername = N'SalesOrderHeader_Employee',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderDetail table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table3,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderHeader table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table2,   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the Employee table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table1,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [アーティクルを削除します。](../../relational-databases/replication/publish/delete-an-article.md)   
 [既存のパブリケーションでのアーティクルの追加と削除](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
