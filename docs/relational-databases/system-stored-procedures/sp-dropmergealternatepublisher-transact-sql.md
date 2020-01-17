---
title: sp_dropmergealternatepublisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
author: stevestein
ms.author: sstein
ms.openlocfilehash: b6938a94b2cfe322abf55cbf663f91b4328c2120
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054292"
---
# <a name="spdropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ パブリケーションから代替パブリッシャーを削除します。 このストアド プロシージャは、サブスクライバーのサブスクリプション データベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` 現在のパブリッシャーの名前です。 *パブリッシャー*は**sysname**、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` 現在のパブリケーション データベースの名前です。 *publisher_db*は**sysname**、既定値はありません。  
  
`[ @publication = ] 'publication'` 現在のパブリケーションの名前です。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @alternate_publisher = ] 'alternate_publisher'` 代替同期パートナーとして削除する代替パブリッシャーの名前です。 *alternate_publisher*は**sysname**、既定値はありません。  
  
`[ @alternate_publisher_db = ] 'alternate_publisher_db'` 代替同期パートナー パブリケーション データベースとして削除するパブリケーション データベースの名前です。 *alternate_publisher_db*は**sysname**、既定値はありません。  
  
`[ @alternate_publication = ] 'alternate_publication'` 代替同期パートナー パブリケーションとして削除するパブリケーションの名前です。 *alternate_publication*は**sysname**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_dropmergealternatepublisher**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_dropmergelternatepublisher**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_addmergealternatepublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
