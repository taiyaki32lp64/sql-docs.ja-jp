---
title: MSSQL_ENG014160 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014160 error
ms.assetid: d0f3855e-d095-4a81-a5bd-9d7ad51f2c77
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 42f0b6894bac639d287eb62f9870d7bfd6daba3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62864847"
---
# <a name="mssqleng014160"></a>MSSQL_ENG014160
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14160|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 このパブリケーションに対する 1 つ以上のサブスクリプションの有効期限が切れています。|  
  
## <a name="explanation"></a>説明  
 レプリケーションでは、いくつかの条件に対して警告を有効にできます。 こうした条件には、サブスクリプションの有効期限の残り時間などがあります。 指定した *保有期間*内にサブスクリプションの同期をとらないと、サブスクリプションの有効期限が切れることがあります。 詳細については、「 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)」をご覧ください。  
  
 レプリケーション モニターまたは [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql)を使用して警告を有効にするときは、警告を表示するタイミングを決定するしきい値を指定します。 指定したしきい値に達するか、そのしきい値を超えた場合、警告がレプリケーション モニターに表示され、イベントが Windows イベント ログに書き込まれます。 しきい値に達した時点で、SQL Server エージェントの警告を表示させることもできます。 詳細については、「[レプリケーション モニターのしきい値と警告の設定](monitor/set-thresholds-and-warnings-in-replication-monitor.md)」および「[プログラムによるレプリケーションの監視](monitoring-replication.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 この問題の解決策は、警告が発生した原因によって異なります。  
  
-   しきい値を超えても、サブスクリプションの有効期限が切れていない場合は、そのサブスクリプションを同期します。 詳細については、「 [データの同期](synchronize-data.md)」を参照してください。  
  
-   エージェントが実行されていても、変更が適切にレプリケートされていない場合は、サブスクリプションの有効期限が切れる可能性があります。 トランザクション レプリケーションの場合は、ディストリビューション エージェントとログ リーダー エージェントが実行されていることを確認します。 マージ レプリケーションの場合は、マージ エージェントが実行されていることを確認します。 これらのエージェントの起動方法については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」および「[レプリケーション エージェント実行可能ファイルの概念](concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
-   サブスクリプションの有効期限が切れている場合、サブスクリプションの種類と期限切れになってからの期間によって、再初期化するか、削除して再作成する必要があります。 詳細については、「 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
