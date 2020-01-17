---
title: sp_replmonitorhelppublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublication_TSQL
- sp_replmonitorhelppublication
helpviewer_keywords:
- sp_replmonitorhelppublication
ms.assetid: 7928c50c-617f-41c5-9e0f-4e42e8be55dc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8dc952f03ea2538412c864e1a9e9b228bf3ca877
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771209"
---
# <a name="spreplmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリッシャー側の 1 つ以上のパブリケーションに関する現在の状態情報を返します。 レプリケーションを監視するために使用されるこのストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorhelppublication [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db'   
    [ , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
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
  
`[ @refreshpolicy = ] refreshpolicy`内部でのみ使用します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|パブリッシャーの名前です。|  
|**レプリケーション**|**sysname**|パブリケーションの名前を指定します。|  
|**publication_type**|**int**|パブリケーションの種類を指定します。次のいずれかの値を指定できます。<br /><br /> **0** = トランザクションパブリケーション<br /><br /> **1** = スナップショットパブリケーション<br /><br /> **2** = マージパブリケーション|  
|**status**|**int**|パブリケーションに関連付けられているすべてのレプリケーション エージェントの状態の最大値です。次のいずれかの値をとります。<br /><br /> **1** = 開始<br /><br /> **2** = 成功<br /><br /> **3** = 実行中<br /><br /> **4** = アイドル<br /><br /> **5** = 再試行中<br /><br /> **6** = 失敗|  
|**warning**|**int**|パブリケーションに属しているサブスクリプションによって生成されるしきい値警告の最大値です。次の 1 つ以上の値の論理和になります。<br /><br /> **1** = 有効期限-トランザクションパブリケーションに対するサブスクリプションが、保有期間のしきい値内に同期されていません。<br /><br /> **2** = 待機時間-トランザクションパブリッシャーからサブスクライバーへのデータのレプリケートにかかった時間が、秒単位のしきい値を超えています。<br /><br /> **4** = mergeexpiration-マージパブリケーションに対するサブスクリプションが、保有期間のしきい値内に同期されていません。<br /><br /> **8** = mergefastrunduration-高速ネットワーク接続経由で、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **16** = mergeslowrunduration-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **32** = mergefastrunspeed-高速ネットワーク接続上で、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でのしきい値の比率を維持できませんでした。<br /><br /> **64** = mergeslowrunspeed-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でしきい値を維持できませんでした。|  
|**worst_latency**|**int**|トランザクションパブリケーションのログリーダーまたはディストリビューションエージェントによって反映されたデータ変更の待機時間の最大値 (秒単位)。|  
|**best_latency**|**int**|トランザクションパブリケーションのログリーダーまたはディストリビューションエージェントによって反映されたデータ変更の最小待機時間 (秒単位)。|  
|**average_latency**|**int**|トランザクションパブリケーションのログリーダーまたはディストリビューションエージェントによって反映されたデータ変更の平均待機時間 (秒単位)。|  
|**last_distsync**|**datetime**|ディストリビューション エージェントが最後に実行された日時です。|  
|**保有**|**int**|パブリケーションの保有期間を示します。|  
|**latencythreshold**|**int**|トランザクションパブリケーションに設定されている待機時間のしきい値です。|  
|**expirationthreshold**|**int**|パブリケーションがマージパブリケーションである場合に、パブリケーションに設定されている有効期限のしきい値です。|  
|**agentnotrunningthreshold**|**int**|エージェントが実行されないようにするための最長時間を設定するしきい値です。|  
|**subscriptioncount**|**int**|パブリケーションに対するサブスクリプションの数を指定します。|  
|**runningdistagentcount**|**int**|パブリケーションに対して実行されているディストリビューションエージェントの数を指定します。|  
|**snapshot_agentname**|**sysname**|パブリケーションのスナップショットエージェントジョブの名前。|  
|**logreader_agentname**|**sysname**|トランザクションパブリケーションのログリーダーエージェントジョブの名前。|  
|**qreader_agentname**|**sysname**|キュー更新をサポートするトランザクションパブリケーションのキューリーダーエージェントジョブの名前。|  
|**worst_runspeedPerf**|**int**|マージパブリケーションの最長同期時間です。|  
|**best_runspeedPerf**|**int**|マージパブリケーションの最短同期時間です。|  
|**average_runspeedPerf**|**int**|マージパブリケーションの平均同期時間です。|  
|**retention_period_unit**|**int**|*保有期間*を表すために使用される単位です。|  
|**パブリッシャー**|**sysname**|パブリケーションをパブリッシュする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replmonitorhelppublication**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replmonitorhelppublication**を実行できるのは、ディストリビューションデータベースの固定データベースロール**db_owner**または**replmonitor**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Programmatically Monitor Replication (プログラムによるレプリケーションの監視)](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
