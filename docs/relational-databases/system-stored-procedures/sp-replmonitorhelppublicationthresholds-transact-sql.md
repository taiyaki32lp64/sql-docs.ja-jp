---
title: sp_replmonitorhelppublicationthresholds (T-sql)
description: 監視されるパブリケーションに設定されたしきい値メトリックを返す sp_replmonitorhelppublicationthresholds ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
author: stevestein
ms.author: sstein
ms.openlocfilehash: d351db8ca696263f294f5a52f364d42ac48bad24
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320779"
---
# <a name="sp_replmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  監視されるパブリケーションに設定されたしきい値メトリックを返します。 レプリケーションを監視するために使用されるこのストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピックリンクアイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-sql 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシュされたデータベースの名前を指定します。 *publisher_db*は**sysname**であり、既定値はありません。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *publication*は**sysname**,、既定値はありません。  
  
`[ @publication_type = ] publication_type`パブリケーションの種類。 *publication_type*は**int**,、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|トランザクションパブリケーション。|  
|**1 で保護されたプロセスとして起動されました**|スナップショットパブリケーション。|  
|**3**|マージ パブリケーションです。|  
|NULL (既定値)|レプリケーションは、パブリケーションの種類を特定しようとします。|  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**metric_id**|**通り**|レプリケーションパフォーマンスメトリックの ID。次のいずれかを指定できます。<br /><br /> **1 有効期限**-トランザクションパブリケーションに対するサブスクリプションの期限が迫っていないかを監視します。<br /><br /> **2latency** -トランザクションパブリケーションに対するサブスクリプションのパフォーマンスを監視します。<br /><br /> **4mergeexpiration 期限**-マージパブリケーションに対するサブスクリプションの期限が迫っていないかを監視します。<br /><br /> **5mergeslowrunduration** -低帯域 (ダイヤルアップ) 接続でのマージ同期の期間を監視します。<br /><br /> **6mergefastrunduration** -高帯域 (LAN) 接続でのマージ同期の期間を監視します。<br /><br /> **7mergefastrunspeed** -高帯域 (LAN) 接続でのマージ同期の同期率を監視します。<br /><br /> **8mergeslowrunspeed** -低帯域 (ダイヤルアップ) 接続でのマージ同期の同期率を監視します。|  
|**題**|**sysname**|レプリケーション パフォーマンス測定基準の名前。|  
|**数値**|**通り**|パフォーマンスメトリックのしきい値。|  
|**shouldalert**|**bit**|メトリックがこのパブリケーションに対して定義されたしきい値を超えた場合にアラートを生成するかどうかを指定します。値**1**は、警告を発生させることを示します。|  
|**isenabled**|**bit**|このパブリケーションのこのレプリケーションパフォーマンスメトリックで監視が有効になっているかどうかを示します。値が**1**の場合は、監視が有効になっていることを示します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replmonitorhelppublicationthresholds**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replmonitorhelppublicationthresholds**を実行できるのは、ディストリビューションデータベースの固定データベースロール**db_owner**または**replmonitor**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [プログラムによるレプリケーションの監視](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
