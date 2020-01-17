---
title: データベース チェックポイント (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- automatic checkpoints
- transaction logs [SQL Server], checkpoints
- logs [SQL Server], active
- pages [SQL Server], dirty
- MinLSN
- checkpoints [SQL Server]
- pages [SQL Server], flushing
- dirty pages
- transaction logs [SQL Server], active logs
- recovery interval option [SQL Server]
- buffer cache [SQL Server]
- logs [SQL Server], checkpoints
- Minimum Recovery LSN
- flushing pages
- active logs
ms.assetid: 98a80238-7409-4708-8a7d-5defd9957185
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33f85b2f1cd8b259e46851aab818b258a6d78291
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206105"
---
# <a name="database-checkpoints-sql-server"></a>データベース チェックポイント (SQL Server)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース チェックポイントについて概説します。 *チェックポイント* によって、予期しないシャットダウンやクラッシュの後の復旧中に、ログに格納されている変更を [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] が適用するための最適なポイントが作成されます。  
  
  
##  <a name="Overview"></a> チェックポイントの概要  
 パフォーマンス向上のため、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では、メモリ (バッファー キャッシュ) にあるデータベース ページが変更されるようになり、ページが変更されるたびにディスクに書き込まれることはなくなりました。 また、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では定期的に各データベースにチェックポイントが発行されます。 *チェックポイント* では、現在メモリにある修正ページ (つまり *ダーティ ページ*) とトランザクション ログ情報がメモリからディスクに書き込まれ、トランザクション ログの情報も記録されます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]では、自動、間接、手動、および内部といったチェックポイントの種類がサポートされています。 次の表は、チェックポイントの種類をまとめたものです。  
  
|名前|[!INCLUDE[tsql](../../includes/tsql-md.md)] インターフェイス|説明|  
|----------|----------------------------------|-----------------|  
|Automatic|EXEC sp_configure **'`recovery interval`'、' *`seconds`* '**|によって予測された上位時間制限を満たすためにバック グラウンドで自動的に発行された、`recovery interval`サーバー構成オプション。 自動チェックポイントは、最後まで実行されます。  自動チェックポイントは、未処理の書き込み数と、20 ミリ秒を超える書き込み待機時間の上昇を[!INCLUDE[ssDE](../../includes/ssde-md.md)]が検出したかどうかに応じて調整されます。<br /><br /> 詳細については、「[recovery interval サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)」を参照してください。|  
|間接|ALTER DATABASE ...SET TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS &#124; MINUTES }|所定のデータベースのユーザーが指定したターゲット復旧時間に合わせて、バック グラウンドで発行されます。 既定のターゲット復旧時間は 0 です。この場合、自動チェックポイント ヒューリスティックがデータベースで使用されます。 ALTER DATABASE を使用して TARGET_RECOVERY_TIME を >0 に設定した場合、サーバー インスタンスに指定された復旧間隔ではなく、この値が使用されます。<br /><br /> 詳細については、「 [データベースのターゲットの復旧時間の変更 &#40;SQL Server&#41;](change-the-target-recovery-time-of-a-database-sql-server.md)サーバー構成オプションを構成する方法について説明します。|  
|手動|CHECKPOINT [ *checkpoint_duration* ]|[!INCLUDE[tsql](../../includes/tsql-md.md)] CHECKPOINT コマンドを実行すると発行されます。 接続している現在のデータベースで手動チェックポイントが作成されます。 既定では、手動のチェックポイントは最後まで実行されます。 調整は自動チェックポイントの場合と同様に行われます。  必要に応じて、 *checkpoint_duration* パラメーターを使用し、チェックポイントを完了するのに必要な時間を秒単位で指定します。<br /><br /> 詳細については、「 [CHECKPOINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql)」を参照してください。|  
|Internal|[なし] :|ディスク イメージがログの現在の状態と一致することを保証するために、バックアップやデータベース スナップショット作成など、さまざまなサーバー操作によって発行されます。|  
  
> [!NOTE]  
>  一部の種類のチェックポイントでは、データベース管理者が `-k`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の詳細設定オプションを使用して、I/O サブシステムのスループットに基づいてチェックポイントの I/O 動作を調整できます。 `-k`セットアップ オプションには、自動チェックポイントと、適用されます-k を手動および内部チェックポイントします。  
  
 自動チェックポイント、手動チェックポイント、および内部チェックポイントでは、データベース復旧中にロールフォワードする必要があるのは、最新チェックポイントの後で行われた修正のみです。 これにより、データベースの復旧にかかる時間が短縮されます。  
  
> [!IMPORTANT]  
>  実行時間の長い、コミットされていないトランザクションがあると、すべての種類のチェックポイントで復旧時間が長くなります。  
  
  
  
###  <a name="InteractionBwnSettings"></a> TARGET_RECOVERY_TIME オプションと 'recovery interval' オプションの相互作用  
 次の表は、サーバーの間の相互作用をまとめたものです**sp_configure'`recovery interval`'** 設定とデータベース固有の ALTER DATABASE.。TARGET_RECOVERY_TIME 設定の相互作用をまとめたものです。  
  
|target_recovery_time|'recovery interval'|使用されるチェックポイントの種類|  
|----------------------------|-------------------------|-----------------------------|  
|0|0|ターゲット復旧間隔が 1 分の自動チェックポイント|  
|0|>0|ターゲット復旧間隔が **sp_configurerecovery interval** オプションのユーザー定義設定によって指定されている自動チェックポイント。|  
|>0|該当なし。|復旧時間が TARGET_RECOVERY_TIME 設定 (秒単位) によって設定されている間接チェックポイント ターゲット|  
  
###  <a name="AutomaticChkpt"></a> 自動チェックポイント  
 自動チェックポイントが毎回ログ レコードの数が数に達すること、[!INCLUDE[ssDE](../../includes/ssde-md.md)]で指定された時間内に処理できる推定、`recovery interval`サーバー構成オプション。 ユーザー定義のターゲット復旧時間が設定されていないすべてのデータベースでは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって自動チェックポイントが生成されます。 自動チェックポイントの頻度によって異なります、`recovery interval`詳細サーバー構成オプションは、特定のサーバー インスタンスがシステムの再起動中にデータベースの復旧に使用する最大時間を指定します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、復旧間隔内に処理できるログ レコードの最大数を推定します。 自動チェックポイントを使用するデータベースのログ レコードが最大数に達すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によってデータベースでチェックポイントが発行されます。 自動チェックポイントの作成間隔は大幅に変わります。 相当量のトランザクション ワークロードがあるデータベースでは、主に読み取り専用操作で使用されるデータベースよりもチェックポイントの作成回数が多くなります。  
  
 また、単純復旧モデルの場合、ログが全体の 70% に達すると自動チェックポイントもキューに登録されます。  
  
 単純復旧モデルでは、ログ トランザクションが何かの要因によって遅れていない限り、自動チェックポイントにより、トランザクション ログの未使用のセクションが切り捨てられます。 反対に、完全復旧モデルおよび一括ログ復旧モデルでは、ログ バックアップ チェーンが確立されると、自動チェックポイントによるログの切り捨ては行われなくなります。 詳細については、「[トランザクションログ &#40;SQL Server&#41;](the-transaction-log-sql-server.md)」を参照してください.  
  
 システム障害の後で所定のデータベースの復旧に必要な時間は、障害発生時点でのダーティ ページを再実行するために必要なランダム I/O の容量に大きく依存します。 つまり、`recovery interval`設定は信頼できません。 正確な復旧間隔がわかりません。 さらに、自動チェックポイントの進行中に、データの一般的な I/O アクティビティが急に著しく増加します。  
  
  
####  <a name="PerformanceImpact"></a> 復旧のパフォーマンスに対する復旧間隔の影響  
 オンライン トランザクション処理 (OLTP) システムの短いトランザクションを使用して`recovery interval`復旧時間を決定する最大の要因です。 ただし、`recovery interval`オプションでは、実行時間の長いトランザクションを元に戻すために必要な時間には影響しません。 指定したよりもかなり長くかかる場合、実行時間の長いトランザクションを含むデータベースの復旧で、`recovery interval`オプション。 たとえば、実行時間の長いトランザクションが、サーバー インスタンスが使用不能になった前に、更新プログラムを実行する 2 つの時間をかけて場合、実際の復旧時間よりも長く、`recovery interval`長いトランザクションを復旧する値。 実行時間が長いトランザクションの復旧時間への影響の詳細については、「 [トランザクション ログ &#40;SQL Server&#41;](the-transaction-log-sql-server.md)」を参照してください。  
  
 通常は、既定値によって復旧の最適なパフォーマンスが得られます。 ただし、次のような状況では recovery interval を変更するとパフォーマンスが向上する可能性があります。  
  
-   実行時間の長いトランザクションがロールバックされていないのに、復旧にかかる時間が常に 1 分を超える場合  
  
-   チェックポイントの回数が多いためにデータベースのパフォーマンスが損なわれていると判断できる場合  
  
 `recovery interval` 設定を長くする場合には、少しずつ値を増やして、そのたびに復旧のパフォーマンスへの影響を評価することをお勧めします。 この方法は、重要なため、として、`recovery interval`設定長くすると、データベースの復旧時間がかかりますを何度も完了します。 変更する場合など`recovery interval`10、約 10 倍するまでにかかるかかります`recovery interval`0 に設定されます。  
  
  
###  <a name="IndirectChkpt"></a> 間接チェックポイント  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]に新たに導入された間接チェックポイントは、自動チェックポイントの代わりに使用できる、構成可能なデータベース レベルのチェックポイントです。 間接チェックポイントでは、自動チェックポイントに比べて、システム障害時の復旧時間が短く、予測可能です。 間接チェックポイントには次の利点があります。  
  
-   間接チェックポイントが構成されたデータベースでオンライン トランザクション ワークロードが生じると、パフォーマンスが低下することがあります。 間接チェックポイントは、ターゲットの復旧時間内でデータベースの回復が完了するように、ダーティ ページの数が特定のしきい値を下回るようにします。 復旧間隔構成オプションは、ダーティ ページ数を使用する間接チェックポイントとは異なり、トランザクション数を使用して復旧時間を決定します。 DML 操作の受信数が多いデータベースで間接チェックポイントが有効な場合、バックグラウンド ライターは積極的にディスクにダーティ バッファーのフラッシュを開始し、回復を実行するのに必要な時間をデータベースのターゲット復旧時間内にすることができます。 これにより、ディスクのサブシステムが I/O のしきい値よりも高い動作をするかまたはその値に近づいた場合、パフォーマンス ボトルネックの原因となる追加の I/O アクティビティが特定のシステムで発生する可能性があります。  
  
-   間接チェックポイントを使用すると、REDO 時のランダム I/O のコストを計算に入れて、データベースの復旧時間を確実に制御できます。 このため、所定のデータベースで、復旧時にサーバー インスタンスが上限内にとどまることができます (実行時間の長いトランザクションによって過度の UNDO 回数が生じる場合以外)。  
  
-   間接チェックポイントでは、ディスクへのダーティ ページの書き込みがバックグラウンドで続けられるため、チェックポイントに関連する I/O の急上昇が少なくなります。  
  
 ただし、間接チェックポイントが構成されたデータベースでオンライン トランザクション ワークロードが生じると、パフォーマンスが低下することがあります。 これは、間接チェックポイントで使用されるバックグラウンド ライターによって、サーバー インスタンスの合計書き込みロードが増える場合があるためです。  
  
  
###  <a name="EventsCausingChkpt"></a> 内部チェックポイント  
 内部チェックポイントは、ディスク イメージがログの現在の状態と一致することを保証するために、さまざまなサーバー コンポーネントによって生成されます。 内部チェックポイントは、次のイベントに応答して生成されます。  
  
-   ALTER DATABASE を使用して、データベース ファイルが追加または削除された場合。  
  
-   データベースのバックアップが作成された場合。  
  
-   DBCC CHECK で明示的または内部的に、データベース スナップショットが作成された場合。  
  
-   データベースのシャットダウンが必要な動作が実行された場合。 たとえば、AUTO_CLOSE が ON に設定されていて、データベースへの最後のユーザー接続が終了した場合、またはデータベースの再起動が必要なデータベース オプションが変更された場合です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) サービスを停止することによって、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが停止します。 どちらの場合でも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの各データベースでチェックポイントが作成されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) がオフラインになった場合。  
  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **サーバー インスタンスで復旧間隔を変更するには**  
  
-   [recovery interval サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)  
  
 **データベースで間接チェックポイントを構成するには**  
  
-   [データベースのターゲットの復旧時間の変更 &#40;SQL Server&#41;](change-the-target-recovery-time-of-a-database-sql-server.md)  
  
 **データベースで手動チェックポイントを発行するには**  
  
-   [CHECKPOINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql)  
  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [トランザクション ログの物理アーキテクチャ](https://technet.microsoft.com/library/ms179355.aspx) (in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] オンライン ブック)  
  
  
## <a name="see-also"></a>関連項目  
 [トランザクション ログ &#40;SQL Server&#41;](the-transaction-log-sql-server.md)  
  
  
