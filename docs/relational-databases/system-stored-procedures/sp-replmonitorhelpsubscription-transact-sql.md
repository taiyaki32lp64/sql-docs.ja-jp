---
title: sp_replmonitorhelpsubscription (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpsubscription_TSQL
- sp_replmonitorhelpsubscription
helpviewer_keywords:
- sp_replmonitorhelpsubscription
ms.assetid: a681b2db-c82d-4624-a10c-396afb0ac42f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 845b9bc59b2232dfa6760087c4a18af84a3c65b7
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68764350"
---
# <a name="sp_replmonitorhelpsubscription-transact-sql"></a>sp_replmonitorhelpsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリッシャー側の 1 つ以上のパブリケーションに属するサブスクリプションの現在の状態情報を返します。サブスクリプションごとに 1 行のデータが返されます。 レプリケーションを監視するために使用されるこのストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorhelpsubscription [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @mode = ] mode ]  
    [ , [ @topnum = ] topnum ]   
    [ , [ @exclude_anonymous = ] exclude_anonymous ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`状態を監視するパブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値は NULL です。 **Null**の場合、ディストリビューターを使用するすべてのパブリッシャーに関する情報が返されます。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシュされたデータベースの名前を指定します。 *publisher_db*は**sysname**,、既定値は NULL です。 NULL の場合、パブリッシャーでパブリッシュされたすべてのデータベースに関する情報が返されます。  
  
`[ @publication = ] 'publication'`監視されているパブリケーションの名前を指定します。 *publication*は**sysname**,、既定値は NULL です。  
  
`[ @publication_type = ] publication_type`パブリケーションの種類。 *publication_type*は**int**,、これらの値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|トランザクションパブリケーション。|  
|**1**|スナップショットパブリケーション。|  
|**2**|マージ パブリケーションです。|  
|NULL (既定値)|レプリケーションは、パブリケーションの種類を特定しようとします。|  
  
`[ @mode = ] mode`サブスクリプションの監視情報を返すときに使用するフィルター処理モードを選択します。 *モード*は**int**,、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0** (既定値)|すべてのサブスクリプションを返します。|  
|**1**|エラーがあるサブスクリプションだけを返します。|  
|**2**|しきい値超過の警告を生成したサブスクリプションだけを返します。|  
|**3**|エラーが発生したか、しきい値メトリック警告が生成されたサブスクリプションのみを返します。|  
|**4**|上位25件の最も低いサブスクリプションを返します。|  
|**5**|最も低い50の実行中のサブスクリプションを返します。|  
|**6**|現在同期されているサブスクリプションのみを返します。|  
|**7**|現在同期していないサブスクリプションだけを返します。|  
  
`[ @topnum = ] topnum`返されるデータの先頭にある、指定された数のサブスクリプションのみに結果セットを制限します。 *topnum*は**int**,、既定値はありません。  
  
`[ @exclude_anonymous = ] exclude_anonymous`匿名プルサブスクリプションを結果セットから除外するかどうかを示します。 *exclude_anonymous*は**ビット**,、既定値は**0**です。値が**1**の場合、匿名サブスクリプションは除外され、値**0**はそれらが含まれることを意味します。  
  
`[ @refreshpolicy = ] refreshpolicy`内部でのみ使用します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**status**|**int**|パブリケーションに関連付けられているすべてのレプリケーションエージェントの状態を調べ、次の順序で見つかった最も高い状態を返します。<br /><br /> **6** = 失敗<br /><br /> **5** = 再試行中<br /><br /> **2** = 停止<br /><br /> **4** = アイドル<br /><br /> **3** = 実行中<br /><br /> **1** = 開始|  
|**warning**|**int**|パブリケーションに属しているサブスクリプションによって生成されるしきい値警告の最大値です。次の 1 つ以上の値の論理和になります。<br /><br /> **1** = 有効期限-トランザクションパブリケーションに対するサブスクリプションが、保有期間のしきい値内に同期されていません。<br /><br /> **2** = 待機時間-トランザクションパブリッシャーからサブスクライバーへのデータのレプリケートにかかった時間が、秒単位のしきい値を超えています。<br /><br /> **4** = mergeexpiration-マージパブリケーションに対するサブスクリプションが、保有期間のしきい値内に同期されていません。<br /><br /> **8** = mergefastrunduration-高速ネットワーク接続経由で、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **16** = mergeslowrunduration-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **32** = mergefastrunspeed-高速ネットワーク接続上で、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でのしきい値の比率を維持できませんでした。<br /><br /> **64** = mergeslowrunspeed-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でしきい値を維持できませんでした。|  
|**subscriber**|**sysname**|サブスクライバーの名前です。|  
|**subscriber_db**|**sysname**|サブスクリプションで使用されるデータベースの名前です。|  
|**publisher_db**|**sysname**|パブリケーション データベースの名前です。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**publication_type**|**int**|パブリケーションの種類を指定します。次のいずれかの値を指定できます。<br /><br /> **0** = トランザクションパブリケーション<br /><br /> **1** = スナップショットパブリケーション<br /><br /> **2** = マージパブリケーション|  
|**subtype**|**int**|サブスクリプションの種類です。次のいずれかの値をとります。<br /><br /> **0** = プッシュ<br /><br /> **1** = プル<br /><br /> **2** = 匿名|  
|**latency**|**int**|トランザクションパブリケーションのログリーダーまたはディストリビューションエージェントによって反映されたデータ変更の待機時間の最大値 (秒単位)。|  
|**latencythreshold**|**int**|トランザクションパブリケーションの最大待機時間です。この値を超えると警告が生成されます。|  
|**agentnotrunning**|**int**|エージェントが実行されていない時間の長さを時間単位で指定します。|  
|**agentnotrunningthreshold**|**int**|エージェントが実行されていない、警告が発生するまでの時間を時間単位で示します。|  
|**timetoexpiration**|**int**|サブスクリプションが同期されていない場合に有効期限が切れるまでの時間を時間単位で示します。|  
|**expirationthreshold**|**int**|サブスクリプションが期限切れになるまでの時間を時間単位で示します。警告が生成されます。|  
|**last_distsync**|**datetime**|ディストリビューションエージェント最後に実行された日時を示します。|  
|**distribution_agentname**|**sysname**|トランザクションパブリケーションに対するサブスクリプションのディストリビューションエージェントジョブの名前を指定します。|  
|**mergeagentname**|**sysname**|マージパブリケーションに対するサブスクリプションのマージエージェントジョブの名前を指定します。|  
|**mergesubscriptionfriendlyname**|**sysname**|サブスクリプションに付けられた表示名です。|  
|**mergeagentlocation**|**sysname**|マージエージェントを実行するサーバーの名前を指定します。|  
|**mergeconnectiontype**|**int**|マージ パブリケーションに対するサブスクリプションの同期時に使用される接続です。次のいずれかの値をとります。<br /><br /> **1** = ローカルエリアネットワーク (LAN)<br /><br /> **2** = ダイヤルアップネットワーク接続<br /><br /> **3** = Web 同期。|  
|**mergePerformance**|**int**|サブスクリプションに対するすべての同期と比較した前回の同期のパフォーマンスです。前回の同期の配信速度を前回までのすべての配信速度の平均で割った値に基づいて算出されます。|  
|**mergerunspeed**|**float**|サブスクリプションの前回の同期の配信率です。|  
|**mergerunduration**|**int**|サブスクリプションの最後の同期を完了する時間の長さです。|  
|**monitorranking 付け**|**int**|結果セットのサブスクリプションを並べ替えるために使用される順位付け値です。次のいずれかの値を指定できます。<br /><br /> トランザクション パブリケーションの場合 :<br /><br /> **60** = エラー<br /><br /> **56** = 警告: パフォーマンスクリティカル<br /><br /> **52** = 警告: 間もなく期限切れまたは期限切れです<br /><br /> **50** = 警告: 初期化されていないサブスクリプション<br /><br /> **40** = 失敗したコマンドを再試行しています<br /><br /> **30** = 実行されていない (成功)<br /><br /> **20** = 実行中 (開始、実行中、またはアイドル状態)<br /><br /> マージパブリケーションの場合:<br /><br /> **60** = エラー<br /><br /> **56** = 警告: パフォーマンスクリティカル<br /><br /> **54** = 警告: 実行時間の長いマージ<br /><br /> **52** = 警告: 間もなく期限切れになります<br /><br /> **50** = 警告: 初期化されていないサブスクリプション<br /><br /> **40** = 失敗したコマンドを再試行しています<br /><br /> **30** = 実行中 (開始、実行中、またはアイドル状態)<br /><br /> **20** = 実行されていない (成功)|  
|**distributionagentjobid**|**binary(16)**|トランザクションパブリケーションに対するサブスクリプションのディストリビューションエージェントジョブの ID。|  
|**mergeagentjobid**|**binary(16)**|マージパブリケーションに対するサブスクリプションのマージエージェントジョブの ID。|  
|**distributionagentid**|**int**|サブスクリプションのディストリビューション エージェント ジョブの ID。|  
|**distributionagentprofileid**|**int**|ディストリビューションエージェントによって使用されるエージェントプロファイルの ID。|  
|**mergeagentid**|**int**|サブスクリプションのマージエージェントジョブの ID。|  
|**mergeagentprofileid**|**int**|マージエージェントによって使用されるエージェントプロファイルの ID。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replmonitorhelpsubscription**は、すべての種類のレプリケーションで使用されます。  
  
 **sp_replmonitorhelpsubscription**は、サブスクリプションの状態の重大度に基づいて結果セットを並べ替えます。これは、 *monitorranking*の値によって決定されます。 たとえば、エラー状態のすべてのサブスクリプションの列は、警告状態のサブスクリプションの列よりも上に並べられます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replmonitorhelpsubscription**を実行できるのは、ディストリビューションデータベースの固定データベースロール**db_owner**または**replmonitor**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Programmatically Monitor Replication (プログラムによるレプリケーションの監視)](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
