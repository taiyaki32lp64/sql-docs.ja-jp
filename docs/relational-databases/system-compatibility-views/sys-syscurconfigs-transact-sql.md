---
title: sys.syscurconfigs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b0fad344831d8073badb2618eb2c34a1cdc2161
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089180"
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在の構成オプションごとに 1 つのエントリを保持します。 また、このビューには、構成構造を表す 4 つのエントリも登録されます。 **syscurconfigs**は、ユーザーが照会時に動的に構築します。 詳細については、次を参照してください。 [sys.sysconfigures &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md)します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**value**|**int**|ユーザーが変更可能な変数の値です。 これは、使用して、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] RECONFIGURE が実行された場合にのみです。|  
|**config**|**smallint**|構成変数番号です。|  
|**comment**|**nvarchar (255)**|この構成オプションの説明です。|  
|**status**|**smallint**|このオプションの状態を表すビットマップです。 次の値があります。<br /><br /> 0 = 静的。 設定はサーバーの再起動時に反映されます。<br /><br /> 1 = 動的。 変数は RECONFIGURE ステートメントの実行時に反映されます。<br /><br /> 2 = 詳細。 変数が表示される場合にのみ、**詳細オプションの表示**設定されます。<br /><br /> 3 = 動的および詳細。|  
  
## <a name="see-also"></a>参照  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
