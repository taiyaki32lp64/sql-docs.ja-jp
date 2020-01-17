---
title: sysdbmaintplans (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
author: stevestein
ms.author: sstein
ms.openlocfilehash: a47ae49ab640b18cbcd7286bc5d95bdc74143aac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029972"
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  次の表に記載されて[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既存の情報を保持するために、以前のバージョンからアップグレードされたインスタンス[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] このテーブルの内容は変更されません。 このテーブルに格納されます、 **msdb**データベース。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|データベース メンテナンス プランの id。|  
|**plan_name**|**sysname**|データベース メンテナンス プランの名前。|  
|**date_created**|**datetime**|データベース メンテナンス プランが作成された日付。|  
|**owner**|**sysname**|データベース メンテナンス プランの所有者です。|  
|**max_history_rows**|**int**|システム テーブル内で、データベース メンテナンス プランの履歴の記録用に割り当てられる行数の最大値。|  
|**remote_history_server**|**sysname**|履歴レポートが書き込まれる先のリモート サーバーの名前。|  
|**max_remote_history_rows**|**int**|履歴レポートが書き込まれる先のリモート サーバー上のシステム テーブルに割り当てられる行数の最大数。|  
|**user_defined_1**|**int**|既定値は NULL|  
|**user_defined_2**|**nvarchar(100)**|既定値は NULL|  
|**user_defined_3**|**datetime**|既定値は NULL|  
|**user_defined_4**|**uniqueidentifier**|既定値は NULL|  
|**log_shipping**|**bit**|ログ配布の状態。<br /><br /> **0** = 無効になっている**1** = 有効になっています。|  
  
  
