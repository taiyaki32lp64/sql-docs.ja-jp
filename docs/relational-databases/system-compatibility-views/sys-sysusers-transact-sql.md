---
title: sys.sysusers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysusers
- sys.sysusers_TSQL
- sysusers_TSQL
- sysusers
dev_langs:
- TSQL
helpviewer_keywords:
- sysusers system table
- sys.sysusers compatibility view
ms.assetid: 5f0e6a8d-c983-44f6-97e9-aab5bff67d18
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b8bec28a2e7778a449cb36aeee81481a311c6b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018063"
---
# <a name="syssysusers-transact-sql"></a>sys.sysusers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  ごとに 1 つの行を含む[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows ユーザー、Windows グループ、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザー、または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース内のロール。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**uid**|**smallint**|このデータベース内で一意のユーザー ID。<br /><br /> 1 = データベースの所有者<br /><br /> オーバーフローまたはユーザーおよびロールの数が 32,767 を超える場合は NULL を返します。|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|このデータベース内で一意なユーザー名またはグループ名です。|  
|**sid**|**varbinary(85)**|このエントリのセキュリティ識別子です。|  
|**ロール**|**varbinary(2048)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|アカウントが追加された日付。|  
|**updatedate**|**datetime**|アカウントが最後に変更された日付。|  
|**altuid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> オーバーフローまたはユーザーおよびロールの数が 32,767 を超える場合は NULL を返します。|  
|**password**|**varbinary(256)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**gid**|**smallint**|このユーザーが所属するグループ ID です。 場合**uid**と同じ**gid**、このエントリは、グループを定義します。 オーバーフローまたはグループとユーザーの合計数が 32,767 を超える場合は NULL を返します。|  
|**environ**|**varchar(255)**|予約済み。|  
|**hasdbaccess**|**int**|1 = アカウントはデータベースにアクセスできます。|  
|**islogin**|**int**|1 = アカウントは、Windows グループ、Windows ユーザー、または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン アカウントを持つユーザー。|  
|**isntname**|**int**|1 = アカウントは、Windows グループまたは Windows ユーザーです。|  
|**isntgroup**|**int**|1 = アカウントは Windows グループ。|  
|**isntuser**|**int**|1 = アカウントは Windows ユーザーです。|  
|**issqluser**|**int**|1 = アカウントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーです。|  
|**isaliased**|**int**|1 = アカウントは別のユーザーの別名です。|  
|**issqlrole**|**int**|1 = アカウントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロールです。|  
|**isapprole**|**int**|1 = アカウントは、アプリケーション ロールです。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
