---
title: MSSQLSERVER_32040 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32040 (Database Engine error)
ms.assetid: 709219b1-f8b2-4696-8923-dd2e91492eb8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 198a58816388a1f5c80b45b776548508f01a1c73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914276"
---
# <a name="mssqlserver32040"></a>MSSQLSERVER_32040
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|32040|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum32040|  
|メッセージ テキスト|'最も古い未送信のトランザクション' の警告が発生しました。 現在の値 '%d' はしきい値 '%d' を上回っています。|  
  
## <a name="explanation"></a>説明  
 このデータベース ミラーリング イベントはプリンシパル サーバー インスタンスで発生し、最も古い未送信のトランザクションの経過期間がユーザー指定のしきい値に達したことを示しています。 通常は、システム パフォーマンスの変化が原因で発生します。 2 つのシステムを接続する帯域幅が縮小したか、負荷が増加しています。  
  
 最も古い未送信のトランザクションの経過期間は、未送信のトランザクションの経過時間 (分) によって判断されるデータ損失の可能性を評価するのに役立つパフォーマンス基準です。 この基準は、特に高パフォーマンス モードのセッションに関連しています。 ただし、パートナー間の接続が切断され、ミラーリングが中断している場合は、高度な安全性モードのセッションにも関係します。  
  
## <a name="user-action"></a>ユーザーの操作  
 プリンシパル サーバー インスタンス、ミラー サーバー インスタンス、および両者のネットワーク接続の負荷が原因になっているかどうかを調査します。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
