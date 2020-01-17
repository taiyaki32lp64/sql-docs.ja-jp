---
title: sys.filetables (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- filetables
- filetables_TSQL
- sys.filetables
- sys.filetables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetables catalog view
ms.assetid: a740be59-cd52-4707-9ad2-5203669a63ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 791bba2f5ec1830e343acff24fd55628a3f13d2e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134002"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  各 FileTable 内の行を返します[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]します。 FileTables について詳しくは、「[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)」をご覧ください。    
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**||オブジェクト ID 番号。 データベース内で一意です。<br /><br /> 詳細については、 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)します。|  
|**is_enabled**|**bit**|1 = FileTable は "有効" 状態です。|  
|**directory_name**|**varchar(255)**|FileTable のルート ディレクトリの名前。|  
|**filename_collation_id**||照合順序識別子、FileTable を定義します。|  
|**filename_collation_name**||照合順序名は、FileTable に対して定義されます。|  
  
## <a name="see-also"></a>関連項目  
 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)   
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
  
  
