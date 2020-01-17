---
title: sys.sysreferences (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysreferences
- sys.sysreferences_TSQL
- sysreferences
- sysreferences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysreferences compatibility view
- sysreferences system table
ms.assetid: 81276f13-202e-4e74-962d-46eb98c98d2e
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3edce02f20a16ebd9814f995f00023f8f3b153de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986494"
---
# <a name="syssysreferences-transact-sql"></a>sys.sysreferences (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  参照される列への FOREIGN KEY 制約定義のマッピングをデータベース内に保持します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|FOREIGN KEY 制約の ID。|  
|**fkeyid**|**int**|参照元テーブルの ID。|  
|**rkeyid**|**int**|参照先のテーブルの ID。|  
|**rkeyindid**|**smallint**|参照されるキー列を含む参照されるテーブルにおける、一意なインデックスのインデックス ID です。|  
|**keycnt**|**smallint**|キーの列の数。|  
|**forkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**fkeydbid**|**smallint**|予約済み。|  
|**rkeydbid**|**smallint**|予約済み。|  
|**fkey1**|**smallint**|参照元の列の列 ID。|  
|**fkey2**|**smallint**|参照元の列の列 ID。|  
|**fkey3**|**smallint**|参照元の列の列 ID。|  
|**fkey4**|**smallint**|参照元の列の列 ID。|  
|**fkey5**|**smallint**|参照元の列の列 ID。|  
|**fkey6**|**smallint**|参照元の列の列 ID。|  
|**fkey7**|**smallint**|参照元の列の列 ID。|  
|**fkey8**|**smallint**|参照元の列の列 ID。|  
|**fkey9**|**smallint**|参照元の列の列 ID。|  
|**fkey10**|**smallint**|参照元の列の列 ID。|  
|**fkey11**|**smallint**|参照元の列の列 ID。|  
|**fkey12**|**smallint**|参照元の列の列 ID。|  
|**fkey13**|**smallint**|参照元の列の列 ID。|  
|**fkey14**|**smallint**|参照元の列の列 ID。|  
|**fkey15**|**smallint**|参照元の列の列 ID。|  
|**fkey16**|**smallint**|参照元の列の列 ID。|  
|**rkey1**|**smallint**|参照先の列の列 ID。|  
|**rkey2**|**smallint**|参照先の列の列 ID。|  
|**rkey3**|**smallint**|参照先の列の列 ID。|  
|**rkey4**|**smallint**|参照先の列の列 ID。|  
|**rkey5**|**smallint**|参照先の列の列 ID。|  
|**rkey6**|**smallint**|参照先の列の列 ID。|  
|**rkey7**|**smallint**|参照先の列の列 ID。|  
|**rkey8**|**smallint**|参照先の列の列 ID。|  
|**rkey9**|**smallint**|参照先の列の列 ID。|  
|**rkey10**|**smallint**|参照先の列の列 ID。|  
|**rkey11**|**smallint**|参照先の列の列 ID。|  
|**rkey12**|**smallint**|参照先の列の列 ID。|  
|**rkey13**|**smallint**|参照先の列の列 ID。|  
|**rkey14**|**smallint**|参照先の列の列 ID。|  
|**rkey15**|**smallint**|参照先の列の列 ID。|  
|**rkey16**|**smallint**|参照先の列の列 ID。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
