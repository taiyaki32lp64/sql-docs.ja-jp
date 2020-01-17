---
title: MSsubscriber_info (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_info_TSQL
- MSsubscriber_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_info system table
ms.assetid: 5ca22f41-6020-4f72-8110-e69baf3447cb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 45065f7cde525d65997df2c97c972d684cadd90f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139821"
---
# <a name="mssubscriber_info-transact-sql"></a>MSsubscriber_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscriber_info**テーブルには、ローカル ディストリビューターからサブスクリプションがプッシュされるパブリッシャー/サブスクライバー ペアごとに 1 つの行が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
 **注**このシステム テーブルは非推奨し、以前のバージョンをサポートするために保持されている[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**subscriber**|**sysname**|サブスクライバーの名前。|  
|**type**|**tinyint**|サブスクライバーの種類:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバー。<br /><br /> **1** = ODBC データ ソース。|  
|**login**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のログインです。 サブスクライバーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証モードで追加されている場合は、暗号化形式で格納されます。|  
|**password**|**nvarchar(524)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のパスワードです。 サブスクライバーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証モードで追加されている場合は、暗号化形式で格納されます。|  
|**description**|**nvarchar (255)**|サブスクライバーの説明。|  
|**security_mode**|**int**|実装されているセキュリティ モードです。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
