---
title: MSSQL_REPL027183 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027183 error
ms.assetid: 52c271ac-1a0e-43d5-85d4-35886d1efd32
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 085a02cbb32ac47925ab47713a2502fd5dd3ea7b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770072"
---
# <a name="mssqlrepl027183"></a>MSSQL_REPL027183
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|27183|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|マージ処理で、パラメーター化された行フィルターを使用して、アーティクル内の変更情報を列挙できませんでした。 このエラーが継続して発生する場合、このプロセスのクエリ タイムアウト値を増やし、パブリケーションの保有期間を減少し、パブリッシュされたテーブルのインデックスを強化してください。|  
  
## <a name="explanation"></a>説明  
 このエラーは、フィルター選択されたパブリケーションでの変更を処理中に、マージ エージェント タイムアウトになると発生します。 このタイムアウトは、次のいずれかの問題点により生じた可能性があります。  
  
-   事前計算済みパーティションの最適化の未使用  
  
-   フィルター選択に使用される列のインデックスの断片化  
  
-   **MSmerge_tombstone**、 **MSmerge_contents**、 **MSmerge_genhistory**などの、大規模なマージ メタデータ テーブル  
  
-   一意キーで結合されていないフィルター選択されたテーブルや多くのテーブルを含む結合フィルター  
  
## <a name="user-action"></a>ユーザーの操作  
 問題を解決するには、以下の操作を実行します。  
  
-   マージ エージェントの **-QueryTimeOut** パラメーターの値を大きくし、エラーの原因となっている根本的な問題に対処する間、処理を継続できるようにします。 エージェント パラメーターは、エージェント プロファイルおよびコマンド ラインで指定できます。 詳細については、以下をご覧ください。  
  
    -   [レプリケーション エージェント プロファイルの操作](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [レプリケーション エージェント実行可能ファイルの概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
-   可能であれば、事前計算済みパーティションの最適化を使用します。 既定では、この最適化は、多くのパブリケーションの要件が満たされている場合に使用されます。 これらの要件の詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。 パブリケーションがこれらの要件を満たしていない場合は、パブリケーションを再設計することを検討してください。  
  
-   パブリケーションの保有期間をできる限り低い設定に指定します。保有期間に達するまで、レプリケーションはパブリケーション データベースおよびサブスクリプション データベースでメタデータをクリーンアップできません。 詳細については、「 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)」を参照してください。  
  
-   マージ レプリケーションのメンテナンスの一環として、マージ レプリケーションと関連するシステム テーブルが拡大しているかを時々確認してください(**MSmerge_contents**、**MSmerge_genhistory**、**MSmerge_tombstone**、**MSmerge_current_partition_mappings**、および **MSmerge_past_partition_mappings**)。 定期的にこれらのテーブルのインデックスを再設定します。 詳細については、「 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
-   フィルター選択に使用する列のインデックスが適切であることを確認し、必要に応じてインデックスを再構築します。 詳細については、「 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
-   一意な列に基づく結合フィルターの **join_unique_key** プロパティを設定します。 詳細については、「 [Join Filters](../../relational-databases/replication/merge/join-filters.md)」を参照してください。  
  
-   結合フィルター階層のテーブル数を制限します。 テーブルが 5 つ以上の結合フィルターを生成する場合は、小さなテーブル、変更されないテーブル、プライマリ参照テーブルはフィルター選択しないという別の解決策を検討してください。 結合フィルターは、サブスクリプション間でパーティション分割する必要のあるテーブル間でのみ使用します。  
  
-   同期を行うまでの間はフィルター選択されたテーブルへの変更を少なくするか、マージ エージェントをより頻繁に実行します。 同期処理のスケジュール設定の詳細については、「 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
