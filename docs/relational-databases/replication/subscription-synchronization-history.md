---
title: サブスクリプション、[同期の履歴] | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.synchhistory.f1
- sql13.rep.monitor.subscription.downlevelsynchhistory.f1
ms.assetid: 85f666f6-14ee-4f19-b385-e5cc508aabe4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 38570e910994e77084777bcc4245ccbb6033d39b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769427"
---
# <a name="subscription-synchronization-history"></a>サブスクリプション、[同期の履歴]
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[同期の履歴]** タブには、マージ エージェントの状態、アーティクル統計、履歴、情報メッセージ、エラー メッセージなど詳細情報が表示されます。  
  
## <a name="options"></a>オプション  
 表示するマージ エージェント セッションを **[表示]** メニューで選択した後、 **[マージ エージェントのセッション]** という名前のグリッドで特定のセッションを選択します。 **[選択されたセッションで処理されるアーティクル]** というラベルの付いたグリッド内に、このセッションの詳細情報が表示されます。  
  
 **[表示]**  
 表示するマージ エージェント セッションを選択します。  
  
 **ステータス**  
 セッションの最後のマージ エージェントの状態です。 表示される状態の種類を、次に示します。  
  
-   [エラー]  
  
-   [完了]  
  
-   [再試行中]  
  
-   実行中  
  
 **Start Time**  
 セッションの開始時刻です。  
  
 **[終了時刻]**  
 セッションの終了時刻です。 エージェントが停止していない場合は、このフィールドは空になっています。  
  
 **Duration**  
 セッションでマージ エージェントが動作した時間の長さです。 この時間は、エージェントが現在実行中の場合は経過時間、エージェントが以前に実行されている場合は合計時間を表します。  
  
 **[アップロードされたコマンド]**  
 マージ エージェント セッションの間にアップロードされた行数です。  
  
 **[ダウンロードされたコマンド]**  
 マージ エージェント セッションの間にダウンロードされた行数です。  
  
 **エラー メッセージ**  
 セッションがエラーで終了した場合、このフィールドにはマージ エージェントによってログに記録された最後のエラー メッセージが表示されます。 セッションがエラーで終了しなかった場合は、このフィールドは空白です。  
  
 **[アーティクル]**  
 パブリケーション内の各アーティクルの名前です。パブリケーション全体に対して以下の処理フェーズがあります。  
  
-   **[初期化]** 。 マージ エージェントを開始することを示しています。スナップショットの適用が行われるサブスクリプションの初期化とは同期しません。  
  
-   **[スキーマの変更と一括挿入]** 。  
  
-   **[パブリッシャーへの変更のアップロード]** 。  
  
-   **[サブスクライバーへの変更のダウンロード]** 。  
  
 これらのフェーズを含めることにより、選択されたセッションで各フェーズにかかった時間と合計時間に対する割合をグリッドに表示できます。  
  
 **[% (合計に対する割合)]**  
 選択されたセッションで各フェーズにかかった時間の合計処理時間に対する割合です。  
  
 **Duration**  
 各処理フェーズにかかった時間の長さです。 この時間は、セッションに対してマージ エージェントが現在実行中の場合は経過時間、マージ エージェントが以前に実行されている場合は合計時間を表します。  
  
 **Inserts**  
 選択されたセッションの該当フェーズで挿入された行数です。  
  
 **Updates**  
 選択されたセッションの該当フェーズで更新された行数です。  
  
 **Deletes**  
 選択されたセッションの該当フェーズで削除された行数です。  
  
 **競合**  
 選択されたセッション内の競合の数です。  
  
 **[スキーマの変更]**  
 選択されたセッション内のスキーマの変更の数です。 パブリケーション データベースからレプリケートされるスキーマの変更、アーティクルの追加または削除、およびアーティクル プロパティまたはパブリケーション プロパティへの変更の結果として、スキーマの変更が発生します。  
  
 **[選択されたセッションの最終メッセージ]**  
 このテキスト領域は、選択されたセッションの最終メッセージを表示します。 エラーが発生している場合は、詳細なエラー情報と、エラー発生時に実行しようとしていたコマンドが表示されます。 エラーに関連する追加コンテンツへのリンクも含まれます。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [レプリケーションの監視](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
