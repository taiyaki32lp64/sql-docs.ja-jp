---
title: MSSQLSERVER_32044 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32044 (Database Engine error)
ms.assetid: f2d073be-d9a1-4837-8a38-028d3e3403bd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c6fd8fceb0ad7f9f724ccfecab8da1c0e34a7f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914159"
---
# <a name="mssqlserver32044"></a>MSSQLSERVER_32044
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|32044|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum32044|  
|メッセージ テキスト|'ミラー コミットのオーバーヘッド' の警告が発生しました。 現在の値 '%d' はしきい値 '%d' を上回っています。|  
  
## <a name="explanation"></a>説明  
 このデータベース ミラーリング イベントはプリンシパル サーバー インスタンスで発生し、データベース ミラーリングが原因で、コミットの合計待機時間がユーザー指定のしきい値に達したか、それを超えたことを示します。 待機時間は、トランザクション数と各トランザクションの待機時間の積です。 たとえば、次の場合は両方には、1000 ミリ秒の待機時間が生成されます。1000 トランザクション * 1 ミリ秒、および 1 つのトランザクション\*1000 (ミリ秒)。 コミットの待機時間が増加するのは、ミラー サーバー インスタンスでのトランザクション数の増加、ログ送信の遅れ、またはログ フラッシュの遅れが原因の可能性があります。  
  
 ミラー コミットのオーバーヘッドの量は、同期操作によって現在のパフォーマンスに与える影響を評価するのに役立つパフォーマンス基準です。 この基準は、高い安全性モードのみに関連しています。 高い安全性モードは同期モードなので、プリンシパル サーバー インスタンスでは、ミラー サーバー インスタンスにログ レコードを送信後、ミラー サーバー インスタンスがディスクにログ レコードを書き込んだことを確認できるまで、トランザクションのコミットを待機します。 ログ レコードは、ミラー データベースへの復元を待機している間は、ミラー サーバー インスタンスのディスクに残ります。  
  
## <a name="user-action"></a>ユーザーの操作  
 プリンシパル サーバー インスタンス、ミラー サーバー インスタンス、および両者のネットワーク接続の負荷が原因になっているかどうかを調査します。  
  
## <a name="see-also"></a>関連項目  
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
