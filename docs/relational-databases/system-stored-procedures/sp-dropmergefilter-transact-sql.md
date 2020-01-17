---
title: sp_dropmergefilter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergefilter_TSQL
- sp_dropmergefilter
helpviewer_keywords:
- sp_dropmergefilter
ms.assetid: 798586d7-05f3-4a5e-bea8-a34b7b52d0fd
author: stevestein
ms.author: sstein
ms.openlocfilehash: b952fcd8145a2cf5392308b21d593e8c377761f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933962"
---
# <a name="spdropmergefilter-transact-sql"></a>sp_dropmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ フィルターを削除します。 **sp_dropmergefilter**削除するマージ フィルターで定義されているすべてのマージ フィルター列を削除します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropmergefilter [ @publication= ] 'publication', [ @article= ] 'article'     , [ @filtername= ] 'filtername'  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @article = ] 'article'` アーティクルの名前です。 *記事*は**sysname**、既定値はありません。  
  
`[ @filtername = ] 'filtername'` 削除するフィルターの名前です。 *filtername*は**sysname**、既定値はありません。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 有効またはスナップショットを無効にする機能を無効にします。 *更によって*は、**ビット**、既定値は、 **0**します。  
  
 **0**スナップショットが無効であることをマージ アーティクルへの変更が発生しないことを指定します。  
  
 **1**マージ アーティクルへの変更、スナップショットを無効になる場合があります。 場合、値があるかどうかは**1**新しいスナップショットを作成する権限が与えられます。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 有効または無効としてサブスクリプションを設定する機能を無効にします。 *更によって*は、**ビット**、既定値は、 **0**します。  
  
 **0**無効になるサブスクリプションをマージ アーティクル フィルターへの変更が発生しないことを指定します。  
  
 **1**と、無効であるサブスクリプションのマージ アーティクルのフィルターを変更することを意味します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_dropmergefilter**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_dropmergefilter**します。  
  
## <a name="see-also"></a>関連項目  
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
