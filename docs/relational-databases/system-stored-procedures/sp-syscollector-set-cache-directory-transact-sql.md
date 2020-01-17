---
title: sp_syscollector_set_cache_directory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_directory_TSQL
- sp_syscollector_set_cache_directory
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_cache_directory stored procedure
ms.assetid: df56d5a5-8961-494f-a745-d752ca63805a
author: stevestein
ms.author: sstein
ms.openlocfilehash: affa8825053f1123c3fae5518f006e2172b9be39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010667"
---
# <a name="spsyscollectorsetcachedirectory-transact-sql"></a>sp_syscollector_set_cache_directory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  管理データ ウェアハウスにアップロードする前に収集されたデータの格納先ディレクトリを指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>引数  
`[ @cache_directory = ] 'cache_directory'` 収集されたデータが一時的に格納されている場所、ファイル システム ディレクトリ。 *cache_directory*は**nvarchar (255)** 既定値は NULL です。 この値を指定しなかった場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定の一時ディレクトリが使用されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 キャッシュ ディレクトリの構成を変更する前に、データ コレクターを無効にする必要があります。 データ コレクターが有効になっている場合、このストアド プロシージャは失敗します。 詳細については、次を参照してください。[有効] または [データ コレクションの無効化](../../relational-databases/data-collection/enable-or-disable-data-collection.md)、および[データ コレクションの管理](../../relational-databases/data-collection/manage-data-collection.md)します。  
  
 sp_syscollector_set_cache_directory の実行時には指定されたディレクトリが存在する必要はありませんが、ディレクトリが作成されるまで、データを正常にキャッシュしてアップロードすることはできません。 このストアド プロシージャを実行する前に、ディレクトリを作成することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) dc_admin 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、データ コレクターを無効にします、キャッシュ ディレクトリを設定するデータ コレクターの`D:\tempdata`、され、データ コレクターを有効になります。  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXEC dbo.sp_syscollector_set_cache_directory N'D:\tempdata';  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
