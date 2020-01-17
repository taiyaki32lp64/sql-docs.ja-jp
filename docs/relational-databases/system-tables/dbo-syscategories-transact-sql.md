---
title: dbo.syscategories (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27056917d828313eaa97ad204d0297cec0fb7995
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084671"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で、ジョブ、警告、オペレーターの分類に使用されるカテゴリを格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|カテゴリの ID。|  
|**category_class**|**int**|カテゴリ内のアイテムの種類。<br /><br /> **1**ジョブを =<br /><br /> **2** = 警告<br /><br /> **3** = 演算子|  
|**category_type**|**tinyint**|カテゴリの種類:<br /><br /> **1** = ローカル<br /><br /> **2** = マルチ サーバー<br /><br /> **3** = なし|  
|**name**|**sysname**|カテゴリの名前。|  
  
  
