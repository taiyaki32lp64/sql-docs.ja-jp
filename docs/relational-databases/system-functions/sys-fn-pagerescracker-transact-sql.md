---
title: sys.fn_PageResCracker (TRANSACT-SQL) |Microsoft Docs
description: Sys.fn_PageResCracker システム関数のドキュメントです。
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_PageResCracker
- sys.fn_PageResCracker_TSQL
- fn_PageResCracker_TSQL
- sys.fn_PageResCracker
- sys.dm_db_page_info
dev_langs:
- TSQL
helpviewer_keywords:
- fn_PageResCracker function
- page_resource
- sys.fn_PageResCracker function
- sys.dm_db_page_info
- page info
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: 6d8203979a0afdca1ae78b9bd51723c906c40ea2
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267074"
---
# <a name="sysfnpagerescracker-transact-sql"></a>sys.fn_PageResCracker (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

返します、 `db_id`、 `file_id`、および`page_id`の指定された`page_resource`値。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>引数  
*page_resource*    
データベース ページのリソースの 8 バイトの 16 進数形式です。
  
## <a name="tables-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|db_id|**int**|データベース ID|  
|file_id|**int**|ファイル ID|  
|page_id|**int**|ページ ID|  
  
## <a name="remarks"></a>コメント  
`sys.fn_PageResCracker` データベースの ID、ID と、ページのページ ID のファイルを含む行セットにデータベース ページの 8 バイトの 16 進形式を変換に使用されます。   

有効なページのリソースを取得することができます、`page_resource`の列、 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)動的管理ビューまたは[sys.sysprocesses &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)システム ビュー。 無効なページ、リソースが使用されている場合、戻り値は NULL です。  
主な用途`sys.fn_PageResCracker`、これらのビュー間の結合を容易にして、 [sys.dm_db_page_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)動的管理関数など、ページに関する情報を取得するには、所属するオブジェクト。
  
## <a name="permissions"></a>アクセス許可  
ユーザーのニーズ`VIEW SERVER STATE`サーバーに対する権限。  
  
## <a name="examples"></a>使用例  
`sys.fn_PageResCracker`関数を組み合わせて使用できる[sys.dm_db_page_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)ページのトラブルシューティングを行うをブロックして待機を関連[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  次のスクリプトでは、これらの関数を使用して、ページのリソースのいくつかの種類で現在待機しているすべてのアクティブな要求のデータベース ページの情報を収集する方法の例を示します。 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_db_page_info &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sys.sysprocesses &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
