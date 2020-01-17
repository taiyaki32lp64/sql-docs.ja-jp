---
title: sys.syslogins (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syslogins_TSQL
- syslogins
- sys.syslogins
- sys.syslogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syslogins compatibility view
- syslogins system table
ms.assetid: 4cb34f17-a4bb-469f-a218-71f074e6308f
author: rothja
ms.author: jroth
ms.openlocfilehash: 5745d3f98741d4a414c7bb69d8f9865258d47e34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020007"
---
# <a name="syssyslogins-transact-sql"></a>sys.syslogins (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログイン アカウントごとに 1 つの行が含まれています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**sid**|**varbinary(85)**|セキュリティ識別子です。|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|ログインが追加された日付です。|  
|**updatedate**|**datetime**|ログインが更新された日付です。|  
|**accdate**|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totcpu**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totio**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**spacelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**timelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resultlimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|ユーザーのログイン名です。|  
|**dbname**|**sysname**|接続が確立されているときに、ユーザーの既定のデータベースの名前です。|  
|**password**|**nvarchar(128)**|NULL を返します。|  
|**language**|**sysname**|ユーザーの既定の言語です。|  
|**denylogin**|**int**|1 = ログインは [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザーまたはグループであり、アクセスは拒否されました。|  
|**hasaccess**|**int**|1 = ログインにサーバーへのアクセスが付与されています。|  
|**isntname**|**int**|1 = ログインは Windows ユーザーまたはグループ。<br /><br /> 0 = ログインは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインです。|  
|**isntgroup**|**int**|1 = ログインは Windows グループです。|  
|**isntuser**|**int**|1 = ログインは Windows ユーザーです。|  
|**sysadmin**|**int**|1 = ログインのメンバーである、 **sysadmin**サーバーの役割。|  
|**securityadmin**|**int**|1 = ログインのメンバーである、 **securityadmin**サーバーの役割。|  
|**serveradmin**|**int**|1 = ログインのメンバーである、 **serveradmin**固定サーバー ロール。|  
|**setupadmin**|**int**|1 = ログインのメンバーである、 **setupadmin**固定サーバー ロール。|  
|**processadmin**|**int**|1 = ログインのメンバーである、 **processadmin**固定サーバー ロール。|  
|**diskadmin**|**int**|1 = ログインのメンバーである、 **diskadmin**固定サーバー ロール。|  
|**dbcreator**|**int**|1 = ログインのメンバーである、 **dbcreator**固定サーバー ロール。|  
|**bulkadmin**|**int**|1 = ログインのメンバーである、 **bulkadmin**固定サーバー ロール。|  
|**loginname**|**nvarchar(128)**|ユーザーのログイン名です。 これは旧バージョンとの互換性のために用意されています。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
