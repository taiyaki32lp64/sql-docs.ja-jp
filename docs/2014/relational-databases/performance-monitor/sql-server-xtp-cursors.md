---
title: XTP Cursors |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b591aa8e89200ca863b1e8196c383c506401fc3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151066"
---
# <a name="xtp-cursors"></a>XTP Cursors
  XTP Cursors パフォーマンス オブジェクトには、XTP エンジンの内部カーソルに関連するカウンターが含まれています。 カーソルとは、XTP エンジンが [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを処理するために使用する、低レベルの構成要素です。 このため、通常はユーザー側でカーソルを直接管理することはありません。  
  
 この表は、 **XTP Cursors**カウンター。  
  
|カウンター|説明|  
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
 [XTP &#40;、インメモリ OLTP&#41;パフォーマンス カウンター](../../integration-services/performance/performance-counters.md)  
  
  
