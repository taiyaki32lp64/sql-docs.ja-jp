---
title: sys.dm_os_stacks (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_stacks
- dm_os_stacks_TSQL
- sys.dm_os_stacks
- sys.dm_os_stacks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_stacks dynamic management view
ms.assetid: a69b06c4-28f0-4535-8fa1-9f132db4d916
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8f287c548a7ebb71b1ebf3e1bce30e43b412c755
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265718"
---
# <a name="sysdmosstacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  この動的管理ビューは内部で使用される[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以下を実行します。  
  
-   保持すると、未処理の割り当てなど、デバッグ データの追跡します。  
  
-   想定または検証で使用されるロジック[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]特定の呼び出しが行われたことを想定の場所でのコンポーネント。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|このスタック割り当ての一意のアドレス。 NULL 値は許可されません。|  
|**frame_index**|**int**|各行は、関数を表す特定のフレーム インデックスを使用して昇順で並べ替えられる場合、呼び出す**stack_address**、完全なコール スタックを返します。 NULL 値は許可されません。|  
|**frame_address**|**varbinary(8)**|関数呼び出しのアドレス。 NULL 値は許可されません。|  
  
## <a name="remarks"></a>コメント  
 **sys.dm_os_stacks**サーバーとその他のコンポーネントのシンボル情報を正しく表示するサーバー上に存在できる必要があります。  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   


## <a name="see-also"></a>関連項目  
  [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
