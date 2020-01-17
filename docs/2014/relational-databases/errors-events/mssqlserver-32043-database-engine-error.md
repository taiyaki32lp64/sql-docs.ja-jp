---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8892eb88a943176a5d99bdada398d004e983658
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914297"
---
# <a name="mssqlserver32043"></a>MSSQLSERVER_32043
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|32043|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum32043|  
|メッセージ テキスト|'復元されていないログ' の警告が発生しました。 現在の値 '%d' はしきい値 '%d' を上回っています。|  
  
## <a name="explanation"></a>説明  
 ミラー サーバー インスタンスで発生したこのデータベース ミラーリング イベントは、復元されていないログの量がユーザー指定のしきい値に達したことを示しています。 通常は、システム パフォーマンスの変化が原因で発生します。 2 つのシステムを接続する帯域幅が縮小したか、負荷が増加しています。  
  
 復元されていないログとは、ミラー サーバー インスタンスで受信してディスクに書き込んだが、ミラー データベースに復元されるのを待機しているログです。 復元されていないログの量 (KB) は、現在のフェールオーバー時間を求めるうえで役立つ、パフォーマンス基準です。 フェールオーバー時間の主要因は、復元されていないログを適用するために必要な時間です。さらに、データベースを復旧してオンラインに復帰するための時間が必要です。  
  
> [!NOTE]  
>  自動フェールオーバーの場合、システムが障害を通知するまでの時間は、フェールオーバー時間に関係ありません。  
  
## <a name="user-action"></a>ユーザーの操作  
 プリンシパル サーバー インスタンス、ミラー サーバー インスタンス、および両者のネットワーク接続の負荷が原因になっているかどうかを調査します。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
