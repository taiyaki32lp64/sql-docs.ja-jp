---
title: アーティクルの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], dropping
- sp_droparticle
- sp_dropmergearticle
- deleting articles
- removing articles
- dropping articles
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: df7163395127b1478762078a74c0552c60e2dd65
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907817"
---
# <a name="delete-an-article"></a>アーティクルの削除
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[tsql](../../../includes/tsql-md.md)] またはレプリケーション管理オブジェクト (RMO) を使用して、アーティクルを削除する方法について説明します。 アーティクルを削除できる条件と、アーティクルを削除するために新しいスナップショットやサブスクリプションの再初期化が必要かどうかについては、「[Add Articles to and Drop Articles from Existing Publications](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)」(既存のパブリケーションでのアーティクルの追加と削除) をご覧ください。  
  
 **このトピックの内容**  
  
-   **アーティクルを削除するために使用するもの:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 アーティクルは、レプリケーション ストアド プロシージャを使用してプログラムで削除できます。 使用するストアド プロシージャは、アーティクルが属するパブリケーションの種類によって異なります。  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションからアーティクルを削除するには  
  
1.  [sp_droparticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) を実行して、 **\@article** で指定されているアーティクルを **\@publication** で指定されているパブリケーションから削除します。 **\@force_invalidate_snapshot** に **1** を指定します。  
  
2.  (省略可) パブリッシュされたオブジェクトをデータベースから完全に削除するには、パブリッシャーのパブリケーション データベースに対して `DROP <objectname>` コマンドを実行します。  

#### <a name="to-delete-an-article-from-a-merge-publication"></a>アーティクルをマージ パブリケーションから削除するには  
  
1.  [sp_dropmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) を実行して、 **\@article** で指定されているアーティクルを **\@publication** で指定されているパブリケーションから削除します。 必要に応じて、 **\@force_invalidate_snapshot** に **1** を指定し、 **\@force_reinit_subscription** に **1** を指定します。  
  
2.  (省略可) パブリッシュされたオブジェクトをデータベースから完全に削除するには、パブリッシャーのパブリケーション データベースに対して `DROP <objectname>` コマンドを実行します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、トランザクション パブリケーションからアーティクルを削除します。 この変更によって既存のスナップショットが無効になるため、 **\@force_invalidate_snapshot** パラメーターに **1** が指定されます。  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article AS sysname;  
SET @publication = N'AdvWorksProductTran';   
SET @article = N'Product';   
  
-- Drop the transactional article.  
USE [AdventureWorks]  
EXEC sp_droparticle   
  @publication = @publication,   
  @article = @article,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
 次の例では、マージ パブリケーションから 2 つのアーティクルを削除します。 この変更によって既存のスナップショットが無効になるため、 **\@force_invalidate_snapshot** パラメーターに **1** が指定されます。  
  
```  
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
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 アーティクルは、レプリケーション管理オブジェクト (RMO) を使用してプログラムから削除できます。 アーティクルを削除する際に使用する RMO のクラスは、アーティクルが属しているパブリケーションの種類によって異なります。  
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのアーティクルを削除するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransArticle> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> の各プロパティを設定します。  
  
4.  手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> プロパティを調べて、アーティクルが存在していることを確認します。 このプロパティの値が **false**の場合、手順 3. で指定したアーティクルのプロパティが正しく定義されていないか、アーティクルが存在していません。  
  
6.  <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> メソッドを呼び出します。  
  
7.  すべての接続を閉じます。  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>マージ パブリケーションのアーティクルを削除するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> の各プロパティを設定します。  
  
4.  手順 1. で作成した接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> プロパティを調べて、アーティクルが存在していることを確認します。 このプロパティの値が **false**の場合、手順 3. で指定したアーティクルのプロパティが正しく定義されていないか、アーティクルが存在していません。  
  
6.  <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> メソッドを呼び出します。  
  
7.  すべての接続を閉じます。  
  
## <a name="see-also"></a>参照  
 [既存のパブリケーションでのアーティクルの追加と削除](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
