---
title: SQL Server の Plan Cache オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Plan Cache object
- SQLServer:Plan Cache
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a181919a40ce2e53c9fef9887f5c7ec6ff93fc5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130845"
---
# <a name="sql-server-plan-cache-object"></a>SQL Server の Plan Cache オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Plan Cache** オブジェクトには、ストアド プロシージャ、アドホックおよび準備済みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメント、トリガーなどのオブジェクトを保存するために、[!INCLUDE[tsql](../../includes/tsql-md.md)] がどのようにメモリを使用しているかを監視するためのカウンターがあります。 **Plan Cache** オブジェクトの複数のインスタンスを同時に監視できます。各インスタンスは、監視される異なる種類のクエリ プランを表します。  
  
 次の表では、 **SQLServer:Plan Cache**カウンターについて説明します。  
  
|SQL Server Plan Cache のカウンター|[説明]|  
|------------------------------------|-----------------|  
|**Cache Hit Ratio**|キャッシュ ヒットとキャッシュ参照の比率。|  
|**Cache Hit Ratio Base**|内部使用のみです。| 
|**Cache Object Counts**|キャッシュ内にあるキャッシュ オブジェクトの数。|  
|**Cache Pages**|キャッシュ オブジェクトによって使用される 8 KB ページの数。|  
|**Cache Objects in use**|使用中のキャッシュ オブジェクトの数。|  
  
 オブジェクトの各カウンターには、次のインスタンスが含まれています。  
  
|Plan Cache インスタンス|[説明]|  
|-------------------------|-----------------|  
|**_Total**|すべての種類のキャッシュ インスタンスの情報。|  
|**Sql Plans**|自動パラメーター化クエリを含むアドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリから作成されたクエリ プランか、 [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_prepare **または** sp_cursorprepare **を使用して準備された**ステートメントから作成されたクエリ プラン。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、後で同一の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが実行された場合の再利用に備えて、アドホック [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのプランをキャッシュに格納します。 ユーザーによるパラメーター化クエリも、明示的に準備されていない場合も含めて Prepared SQL Plans として監視されます。|  
|**Object Plans**|ストアド プロシージャ、関数、またはトリガーの作成によって生成されたクエリ プラン。|  
|**Bound Trees**|ビュー、規則、計算済みの列、および CHECK 制約のための正規化ツリー。|  
|**拡張ストアド プロシージャ**|拡張ストアド プロシージャのカタログ情報。|  
|**Temporary Tables & Table Variables**|一時テーブルおよびテーブル変数に関連するキャッシュ情報。|  
  
## <a name="see-also"></a>参照  
 [サーバー メモリに関するサーバー構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server: Buffer Manager オブジェクト](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
