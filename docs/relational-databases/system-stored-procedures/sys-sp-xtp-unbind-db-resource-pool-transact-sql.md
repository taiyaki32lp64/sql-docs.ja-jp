---
title: sys.sp_xtp_unbind_db_resource_pool (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xtp_unbind_db_resource_pool_TSQL
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool_TSQL
- sys.sp_xtp_unbind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool
ms.assetid: 695a796d-087e-4bc8-99d0-ddc342604c75
author: stevestein
ms.author: sstein
ms.openlocfilehash: be0f8e7b410abb2e9027ce0b773d1a1ad5a14465
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041003"
---
# <a name="sysspxtpunbinddbresourcepool-transact-sql"></a>sys.sp_xtp_unbind_db_resource_pool (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  このシステム ストアド プロシージャは、追跡の目的でデータベースとリソース プールの既存のバインドを削除します。[!INCLUDE[hek_2](../../includes/hek-2-md.md)]メモリ使用量。  指定したデータベースに現在バインドされたプールがない場合、成功が返されます。 データベースがバインドされている場合は、メモリ最適化オブジェクトの以前に割り当てられたメモリは以前のリソース プールに割り当てられたままです。 割り当てられたメモリを解放するデータベースを再起動する必要があります。 リソース プールからデータベースをバインドすることが解除されると、バインドは既定のリソース プールを行います。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'database_name'  
```  
  
## <a name="arguments"></a>引数  
 database_name  
 既存の名前[!INCLUDE[hek_2](../../includes/hek-2-md.md)]データベースを有効にします。  
  
#### <a name="parameters"></a>パラメーター  
  
## <a name="messages"></a>Messages  
 かどうかは、データベースが名前付きリソース プールにバインドされた、プロシージャは正常に終了します。 ただし、データベースを有効にするバインド解除を再起動する必要があります。  
 指定したデータベースに既存のバインドが存在しない場合、`sp_xtp_unbind_db_resource_pool` は正常に終了しますが、次のような情報メッセージが表示されます。  
  
```  
Msg 41374, Level 16, State 1, Procedure sp_xtp_unbind_db_resource_pool_internal, Line 140.  
Database 'Hekaton_DB' does not have a binding to a resource pool.  
  
```  
  
## <a name="example"></a>例  
 次のコードは、バインドされた[!INCLUDE[hek_2](../../includes/hek-2-md.md)] リソース プールからデータベース Hekaton_DB をバインド解除します。  Hekaton_DB が[!INCLUDE[hek_2](../../includes/hek-2-md.md)] リソース プールに現在バインドされていない場合、メッセージが表示されます。 バインドの解除を有効にするにはデータベースを再起動する必要があります。  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'Hekaton_DB'  
```  
  
## <a name="requirements"></a>必要条件  
  
-   指定されるデータベース`database_name`へのバインドがあります、[!INCLUDE[hek_2](../../includes/hek-2-md.md)]リソース プール。  
  
-   CONTROL SERVER 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [データベースを作成してリソース プールにバインドする方法については、「](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)  
  
  
