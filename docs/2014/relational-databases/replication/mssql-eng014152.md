---
title: MSSQL_ENG014152 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014152 error
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e14c0d724ba4832dfc0f67deec25308804b82f84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191427"
---
# <a name="mssqleng014152"></a>MSSQL_ENG014152
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14152|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|レプリケーション-%s: エージェント %s には再試行のスケジュールが設定されました。 %s|  
  
## <a name="explanation"></a>説明  
 指定されたレプリケーション エージェントは、要求された操作を再試行するようにスケジュール設定されました。 ジョブ ステップに設定された再試行の最大回数に達するまで、このプロセスが繰り返し再試行されます。  
  
 通常、再試行は次のいずれかの理由により発生します。  
  
-   **QueryTimeout** 値を超過する。  
  
-   **LoginTimeout** 値を超過する。  
  
-   レプリケーション プロセスがデッドロックの対象として選択される。  
  
## <a name="user-action"></a>ユーザーの操作  
 この再試行のメッセージの発生頻度が低い場合、ユーザー操作は不要です。  
  
 [sp_help_jobstep](/sql/relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql) を使用して、指定されたレプリケーション エージェントの **[エージェントを実行します。]** ステップが再試行される最大回数の現在の設定を表示します。 [sp_update_jobstep](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) ストアド プロシージャの **@retry_attempts** パラメーターを使用して、ジョブ ステップが再試行される回数を調整することができます。  
  
 再試行のメッセージが頻繁に表示される場合は、再試行が発生するメッセージに基づく問題のトラブルシューティングを行います。 エージェントの履歴で、再試行をスケジュール設定する必要があった理由を示すメッセージを確認します。 場合によっては、レプリケーション エージェントに対してより詳細なログ記録を有効にする必要があります。 レプリケーションのログ記録を構成する方法については、サポート技術情報の資料 [312292](https://support.microsoft.com/kb/312292)を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
