---
title: sys.database_automatic_tuning_options (TRANSACT-SQL) |Microsoft Docs
description: SQL Database 自動チューニング オプションを表示する方法について説明します
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs:
- TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 437dbbc4ea7deb32a9723febb443cc67941fdc5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940225"
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>sys.database\_自動\_tuning_options (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  このデータベースの自動チューニング オプションを返します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|自動チューニング オプションの名前。 参照してください[AUTOMATIC_TUNING 設定データベースの ALTER &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)の使用可能なオプションです。|  
|**desired_state**|**smallint**|ユーザーによって明示的に設定の自動チューニング オプションの目的の操作モードを示します。<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|自動チューニング オプションの目的の操作モードの説明テキストです。<br />OFF<br />ON|  
|**actual_state**|**smallint**|自動チューニング オプションの操作モードを示します。<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|自動チューニング オプションの実際の操作モードの説明テキストです。<br />OFF<br />ON|  
|**reason**|**smallint**|実際、目的の状態が異なる理由を示します。<br />2 = 無効になっています<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|なぜ実際と目的の状態が異なる理由の説明テキストです。<br />無効になっている = オプションはシステムによって無効になります。<br />QUERY_STORE_OFF = クエリ ストアがになっています<br />QUERY_STORE_READ_ONLY = クエリ ストアが読み取り専用モード<br />NOT_SUPPORTED = 利用可能でのみ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise edition| 
  
## <a name="permissions"></a>アクセス許可  
 `VIEW DATABASE STATE` アクセス許可が必要です。  
  
## <a name="see-also"></a>関連項目  
 [自動チューニング](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
