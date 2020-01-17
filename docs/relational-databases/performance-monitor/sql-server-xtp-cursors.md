---
title: SQL Server の XTP Cursors | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2920b0f21cca13272b8d8678106d0d231ad56e41
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947821"
---
# <a name="sql-server-xtp-cursors"></a>SQL Server の XTP Cursors
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP Cursors パフォーマンス オブジェクトには、インメモリ OLTP エンジンの内部カーソルに関連するカウンターが含まれています。 カーソルとは、インメモリ OLTP エンジンが [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを処理するために使用する、低レベルの構成要素です。 このため、通常はユーザー側でカーソルを直接管理することはありません。  
  
 次の表で、 **SQL Server の XTP Cursors** カウンターについて説明します。  
  
|カウンター|[説明]|  
|-------------|-----------------|  
|**Cursor deletes/sec**|カーソルの削除回数に関する 1 秒あたりの平均です。|  
|**Cursor inserts/sec**|カーソルの挿入回数に関する 1 秒あたりの平均です。|  
|**Cursor scans started /sec**|カーソル スキャンが開始された回数に関する 1 秒あたりの平均です。|  
|**Cursor unique violations/sec**|UNIQUE 制約の違反に関する 1 秒あたりの平均です。|  
|**Cursor updates/sec**|カーソルの更新回数に関する 1 秒あたりの平均です。|  
|**Cursor write conflicts/sec**|同じ行バージョンに対する書き込み - 書き込みの競合回数に関する 1 秒あたりの平均です。|  
|**Dusty corner scan retries/sec (user-issued)**|ユーザーのフル テーブル スキャンによって発行されたダスティ コーナー スウィープ (詳細なクリーンアップ) の実行中に、書き込みの競合が原因で発生したスキャン再試行回数に関する 1 秒あたりの平均です。 これは非常に低レベルのカウンターであり、お客様による使用は想定されていません。|  
|**Expired rows removed/sec**|カーソルによって削除された、有効期限切れの行の数に関する 1 秒あたりの平均です。|  
|**Expired rows touched/sec**|カーソルによって操作された、有効期限切れの行の数に関する 1 秒あたりの平均です。|  
|**Rows returned/sec**|カーソルによって返された、有効期限切れの行の数に関する 1 秒あたりの平均です。|  
|**Rows touched/sec**|カーソルによって操作された行の数に関する 1 秒あたりの平均です。|  
|**Tentatively-deleted rows touched/sec**|カーソルによって操作された、間もなく期限切れになる行の数に関する 1 秒あたりの平均です。 行が間もなく期限切れになるのは、その行を削除したトランザクションが依然としてアクティブな場合 (つまり、コミットや中止がまだ行われていない場合) です。|  
  
## <a name="see-also"></a>参照  
 [SQL Server XTP &#40;インメモリ OLTP&#41; パフォーマンス カウンター](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
