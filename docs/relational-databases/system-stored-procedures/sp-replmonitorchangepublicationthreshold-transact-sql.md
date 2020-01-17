---
title: sp_replmonitorchangepublicationthreshold (T-sql)
description: パブリケーションの監視しきい値メトリックを変更する sp_replmonitorchangepublicationthreshold ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
author: stevestein
ms.author: sstein
ms.openlocfilehash: fdcf5a9dcd462562886c7815b500c43145b749a3
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322229"
---
# <a name="sp_replmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリケーションの監視しきい値を変更します。 レプリケーションを監視するために使用されるこのストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピックリンクアイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-sql 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシュされたデータベースの名前を指定します。 *publisher_db*は**sysname**であり、既定値はありません。  
  
`[ @publication = ] 'publication'`監視しきい値属性を変更するパブリケーションの名前を指定します。 *publication*は**sysname**,、既定値はありません。  
  
`[ @publication_type = ] publication_type`パブリケーションの種類。 *publication_type*は**int**,、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|トランザクションパブリケーション。|  
|**1 で保護されたプロセスとして起動されました**|スナップショットパブリケーション。|  
|**3**|マージ パブリケーションです。|  
|NULL (既定値)|レプリケーションは、パブリケーションの種類を特定しようとします。|  
  
`[ @metric_id = ] metric_id`変更するパブリケーションしきい値の ID を示します。 *metric_id*は**int**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|値|メトリックの名前|  
|-----------|-----------------|  
|**1 で保護されたプロセスとして起動されました**|**有効期限**-トランザクションパブリケーションに対するサブスクリプションの期限が迫っていないかを監視します。|  
|**3**|**latency** -トランザクションパブリケーションに対するサブスクリプションのパフォーマンスを監視します。|  
|**4/4**|**mergeexpiration 期限**-マージパブリケーションに対するサブスクリプションの期限が迫っていないかを監視します。|  
|**5/5**|**mergeslowrunduration** -低帯域 (ダイヤルアップ) 接続でのマージ同期の期間を監視します。|  
|**6**|**mergefastrunduration** -高帯域幅ローカルエリアネットワーク (LAN) 接続でのマージ同期の期間を監視します。|  
|**7**|**mergefastrunspeed** -高帯域 (LAN) 接続でのマージ同期の同期率を監視します。|  
|**8**|**mergeslowrunspeed** -低帯域 (ダイヤルアップ) 接続でのマージ同期の同期率を監視します。|  
  
 *Metric_id*または*thresholdmetricname*のいずれかを指定する必要があります。 *Thresholdmetricname*を指定する場合は、 *metric_id*を NULL にする必要があります。  
  
`[ @thresholdmetricname = ] 'thresholdmetricname'`変更するパブリケーションしきい値の名前を指定します。 *thresholdmetricname*は**sysname**,、既定値は NULL です。 *Thresholdmetricname*または*metric_id*のいずれかを指定する必要があります。 *Metric_id*が指定されている場合は、 *thresholdmetricname*を NULL にする必要があります。  
  
`[ @value = ] value`パブリケーションしきい値の新しい値を指定します。 *値*は**int**,、既定値は NULL です。 **Null**の場合、メトリック値は更新されません。  
  
`[ @shouldalert = ] shouldalert`パブリケーションのしきい値に達したときにアラートを生成するかどうかを示します。 *alert*は**ビット**,、既定値は NULL です。 値**1**は警告が生成されることを意味し、値**0**は警告が生成されないことを意味します。  
  
`[ @mode = ] mode`パブリケーションのしきい値メトリックが有効な場合はです。 *モード*は**tinyint**,、既定値は**1**です。 値**1**はこのメトリックの監視が有効になっていることを示し、値**2**はこのメトリックの監視が無効になっていることを意味します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replmonitorchangepublicationthreshold**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replmonitorchangepublicationthreshold**を実行できるのは、ディストリビューションデータベースの固定データベースロール**db_owner**または**replmonitor**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [プログラムによるレプリケーションの監視](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
