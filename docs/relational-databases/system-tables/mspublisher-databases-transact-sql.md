---
title: MSpublisher_databases (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
author: stevestein
ms.author: sstein
ms.openlocfilehash: da208c7fb83053c1817693bb16d16c3488fe90c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032613"
---
# <a name="mspublisher_databases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublisher_databases**テーブルには、ローカル ディストリビューターによって処理されるパブリッシャー/パブリッシャー データベースの各ペアの 1 つの行が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前。|  
|**id**|**int**|行の ID。|  
|**publisher_engine_edition**|**int**|エディション、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]発行元は、次のいずれかを指定できます。<br /><br /> **10** = Personal Edition<br /><br /> **11** = Desktop Engine (MSDE)<br /><br /> **20** = Standard<br /><br /> **21** = Workgroup<br /><br /> **30** = Enterprise (評価)<br /><br /> **31** = Developer<br /><br /> **40** = Express (Express は、パブリッシャーにはなれません。 この値は完全性のために存在します。)|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
