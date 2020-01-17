---
title: SQL Server の Columnstore オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 334a8388b7abc217123071fdc37c9e1091f6a3fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987135"
---
# <a name="sql-server-columnstore-object"></a>SQL Server の Columnstore オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **SQLServer:Columnstore** オブジェクトは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で列ストア インデックスの実行を監視するカウンターを提供します。  
  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Columnstore** カウンターについて説明します。  
  
|Columnstore カウンター|[説明]|  
|--------------------------|-----------------|  
|**閉じられたデルタ行グループ数**|閉じられたデルタ行グループの数。|  
|**圧縮されたデルタ行グループ数**|圧縮されたデルタ行グループの数。|  
|**作成されたデルタ行グループ数**|作成されたデルタ行グループの数。|  
|**セグメント キャッシュ ヒット率**|ディスクから読み取らずに、columnstore プール内で見つかった列セグメントのパーセンテージ。|  
|**セグメント キャッシュ ヒット率ベース**|内部使用のみです。|
|**セグメント読み取り数/秒**|物理セグメント読み取りの発生回数。|  
|**削除バッファーの合計移行回数**|組ムーバーが削除バッファーをクリーンアップした回数。|  
|**マージ ポリシーの合計評価数**|columnstore のマージ ポリシーを評価した回数。|  
|**圧縮された行グループ合計数**|圧縮された行グループの合計数。|  
|**マージに適した行グループ合計数**|SQL Server の開始以降 MERGE に適したソースの行グループ数。|  
|**マージと圧縮が行われた行グループ合計数**|SQL Server の起動以降に MERGE で作成された圧縮ターゲット行グループの数。|  
|**マージされたソース行グループ合計数**|SQL Server の起動以降にマージされたソース行グループの数。|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
