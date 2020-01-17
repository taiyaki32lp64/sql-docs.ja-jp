---
title: FT:Crawl Aborted イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Crawl Aborted event class
ms.assetid: eead8ea6-5051-4689-ab30-4dfbfda01fb9
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df18d75f240b4447579a84ad023ecee9757feeb4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089349"
---
# <a name="ftcrawl-aborted-event-class"></a>FT:Crawl Aborted イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **FT:Crawl Aborted** イベント クラスは、フルテキスト クロール中に例外が発生したことを示します。 通常、このエラーは、フルテキスト クロールを停止する原因になります。 詳細なエラー情報については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows イベント ログまたはクロール ログを確認してください。  
  
## <a name="ftcrawl-aborted-event-class-data-columns"></a>FT:Crawl Aborted イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|フルテキスト クロールを実行しているデータベースの ID。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**Error**|**int**|特定のイベントのエラー番号。 多くの場合、 **sysmessages** テーブルに保存されているエラー番号です。|31|はい|  
|**EventClass**|**int**|イベントの種類 = 157。|27|いいえ|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|はい|  
|**Exchange Spill**|**int**|エラー発生時にフルテキスト クロールが実行されているオブジェクトのシステム割り当て ID。|22|はい|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|はい|  
|**SPID**|**int**|イベントが発生したセッションの ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**状態**|**int**|エラーの状態コードと同じです。|30|はい|  
|**TransactionID**|**bigint**|システムによって割り当てられたトランザクション ID。|4|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
