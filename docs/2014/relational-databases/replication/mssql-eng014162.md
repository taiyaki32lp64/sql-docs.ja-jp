---
title: MSSQL_ENG014162 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014162 error
ms.assetid: a15eef3f-219f-45d3-8286-6a864c85a723
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90a0fdb76c93500ba4472ed1082f6c54e56d1f3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63131695"
---
# <a name="mssqleng014162"></a>MSSQL_ENG014162
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14162|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 マージ エージェントが実行されており、必要な要件に適合することを確認してください。|  
  
## <a name="explanation"></a>説明  
 レプリケーションでは、いくつかの条件に対して警告を有効にできます。 たとえば、マージ パブリッシャーとサブスクライバーの間で変更を同期する時間が指定の長さを超えた場合などです。 LAN 接続とダイヤルアップ接続には異なる時間を指定できます。  
  
 レプリケーション モニターまたは [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql)を使用して警告を有効にするときは、警告を表示するタイミングを決定するしきい値を指定します。 指定したしきい値に達するか、そのしきい値を超えた場合、警告がレプリケーション モニターに表示され、イベントが Windows イベント ログに書き込まれます。 しきい値に達した時点で、SQL Server エージェントの警告を表示させることもできます。 詳細については、「[レプリケーション モニターのしきい値と警告の設定](monitor/set-thresholds-and-warnings-in-replication-monitor.md)」および「[プログラムによるレプリケーションの監視](monitoring-replication.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 サブスクリプションが期間のしきい値を超えた場合は、システムでパフォーマンスの問題が発生しているかどうか、またはしきい値を調整する必要があるかどうかを確認する必要があります。 レプリケーションを構成したら、パフォーマンス基準を策定します。これにより、アプリケーションおよびトポロジにおける通常のワークロードに対するレプリケーションの動作方法について判断できるようになります。 このパフォーマンス基準には同期の期間を組み入れ、適切なしきい値を設定できるようにします。  
  
 しきい値が適切でも、その値を超えた場合は、システム内のパフォーマンスのボトルネックになる部分を特定する必要があります。 レプリケーション パフォーマンスの監視とトラブルシューティングを行う方法の詳細については、次のトピックを参照してください。  
  
-   [レプリケーション モニターを使用したパフォーマンスの監視](monitor/monitor-performance-with-replication-monitor.md) (特に、「マージ レプリケーションの詳細な同期パフォーマンスの表示」)  
  
## <a name="see-also"></a>関連項目  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
