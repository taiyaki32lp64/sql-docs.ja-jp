---
title: MSSQL_REPL027056 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 20586254516f97552f3dbc181bc482f24a683d00
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68764843"
---
# <a name="mssqlrepl027056"></a>MSSQL_REPL027056
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|27056|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|マージ プロセスが、'%1' で生成履歴を変更できませんでした。 トラブルシューティングを行うには、詳細な履歴ログとの同期を再開して、書き込み先の出力ファイルを指定してください。|  
  
## <a name="explanation"></a>説明  
 通常このエラーは、極端に大きくなったマージ レプリケーション システム テーブルにおける競合の結果として発生します。 一般的にシステム テーブルは、パブリケーションの保有期間が長いと大きくなります。これは、保有期間が終了するまでメタデータを格納しておく必要があるためです。  
  
## <a name="user-action"></a>ユーザーの操作  
 **問題を解決するには、以下の操作を実行します。**  
  
1.  マージ エージェントの**DownloadGenerationsPerBatch** パラメーターと **UploadGenerationsPerBatch** パラメーターの値を小さくし、エラーの原因となっている根本的な問題に対処する間、処理を継続できるようにします。 エージェント パラメーターは、エージェント プロファイルおよびコマンド ラインで指定できます。 詳細については、以下をご覧ください。  
  
    -   [レプリケーション エージェント プロファイルの操作](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)に割り当てるメモリの最大容量と最小容量を設定する。  
  
2.  パブリケーションの保有期間をできるだけ短く設定します。 詳細については、「 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)」を参照してください。  
  
3.  マージ レプリケーションのメンテナンスの一環として、マージ レプリケーションと関連するシステム テーブルが拡大しているかを時々確認してください(**MSmerge_contents**、**MSmerge_genhistory**、**MSmerge_tombstone**、**MSmerge_current_partition_mappings**、および **MSmerge_past_partition_mappings**)。 定期的にこれらのテーブルのインデックスを再設定します。 詳細については、「 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
