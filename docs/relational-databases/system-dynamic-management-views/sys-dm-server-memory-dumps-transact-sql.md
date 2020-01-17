---
title: sys.dm_server_memory_dumps (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_server_memory_dumps_TSQL
- dm_server_memory_dumps_TSQL
- dm_server_memory_dumps
- sys.dm_server_memory_dumps
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_memory_dumps dynamic management view
ms.assetid: 41782719-f54d-4e11-941a-c050c7576e23
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7f31bc59e918a2a2ca4f0cf9e3833571028e85a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090798"
---
# <a name="sysdmservermemorydumps-transact-sql"></a>sys.dm_server_memory_dumps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  によって生成されたメモリ ダンプのファイルごとに 1 つの行を返します、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]します。 この動的管理ビューを使用して、潜在的な問題のトラブルシューティングを行います。  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**filename**|**nvarchar (256)**|パスと、メモリ ダンプ ファイルの名前。 null にすることはできません。|  
|**creation_time**|**datetimeoffset(7)**|ファイルが作成された日付と時刻。 null にすることはできません。|  
|**size_in_bytes**|**bigint**|ファイルのサイズをバイト単位で。 NULL 値が許可されます。|  
  
## <a name="general-remarks"></a>全般的な解説  
 ダンプの種類として、ミニダンプ、すべてのスレッドのダンプ、または完全なダンプを使用できます。 ファイルがある、拡張子は .mdmp です。  
  
## <a name="security"></a>セキュリティ  
 ダンプ ファイルには機密情報が含まれている場合があります。 機密情報を保護するには、アクセス制御リスト (ACL) を使用してこのファイルへのアクセスを制限するか、アクセスが制限されたフォルダーにファイルをコピーすることができます。 たとえば、デバッグ ファイルを Microsoft サポート サービスに送信する前に、機密情報を削除することお勧めします。  
  
### <a name="permissions"></a>アクセス許可  
 VIEW SERVER STATE 権限が必要です。  
  
  
