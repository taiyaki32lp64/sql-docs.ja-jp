---
title: sp_replmonitorhelpmergesessiondetail (T-sql)
description: 特定のレプリケーションマージエージェントセッションに関する詳細なアーティクルレベル情報を返す sp_replmonitorhelpmergesessiondetail ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesessiondetail
- sp_replmonitorhelpmergesessiondetail_TSQL
helpviewer_keywords:
- sp_replmonitorhelpmergesessiondetail
ms.assetid: 805c92fc-3169-410c-984d-f37e063b791d
author: stevestein
ms.author: sstein
ms.openlocfilehash: b5e29916d4dc8419311c9639cc5321b1cf391940
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321623"
---
# <a name="sp_replmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  マージ レプリケーションの監視に使用する特定のレプリケーション マージ エージェント セッションに関するアーティクル レベルの詳細情報を返します。 結果セットには、セッション中に同期された各アーティクルの詳細行が含まれます。 また、セッションの初期化を表す行や、セッションのアップロードおよびダウンロード フェーズの両方を要約した行も含まれます。 このストアドプロシージャは、ディストリビューター側でディストリビューションデータベースに対して実行されるか、サブスクライバー側でサブスクリプションデータベースに対して実行されます。  
  
 ![トピックリンクアイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-sql 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>引数  
`[ @session_id = ] session_id`エージェントセッションを指定します。 *session_id*は**int**で、既定値はありません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**通り**|同期セッションのフェーズです。次のいずれかの値をとります。<br /><br /> **0** = 初期化行または集計行<br /><br /> **1** = アップロード<br /><br /> **2** = ダウンロード|  
|**ArticleName**|**sysname**|同期するアーティクルの名前を指定します。 **ArticleName**には、アーティクルの詳細を表さない結果セット内の行の概要情報も含まれています。|  
|**PercentComplete**|**位**|現在実行中のセッションまたは失敗したセッションに関する特定のアーティクル詳細行で適用された合計変更のパーセントを示します。|  
|**RelativeCost**|**位**|セッションの合計同期時間に対する割合として、アーティクルの同期に要した時間を示します。|  
|**全**|**通り**|エージェント セッションの長さです。|  
|**ます**|**通り**|セッションの挿入数。|  
|**版**|**通り**|セッションにおける更新数です。|  
|**削除**|**通り**|セッションにおける削除数です。|  
|**競合**|**通り**|セッションで発生した競合の数。|  
|**ErrorID**|**通り**|セッションエラーの ID。|  
|**SeqNo**|**通り**|結果セット内のセッションの順序です。|  
|**RowType**|**通り**|結果セットの各行が表す情報の種類を示します。<br /><br /> **0** = 初期化<br /><br /> **1** = アップロードの概要<br /><br /> **2** = アーティクルのアップロードの詳細<br /><br /> **3** = ダウンロードの概要<br /><br /> **4** = アーティクルのダウンロードの詳細|  
|**SchemaChanges**|**通り**|セッションでのスキーマ変更の数。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replmonitorhelpmergesessiondetail**は、マージレプリケーションの監視に使用されます。  
  
 サブスクライバーで実行された場合、 **sp_replmonitorhelpmergesessiondetail**は、最後の5つのマージエージェントセッションに関する詳細情報のみを返します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replmonitorhelpmergesessiondetail**を実行できるのは、ディストリビューター側のディストリビューションデータベースまたはサブスクライバー側のサブスクリプションデータベースで、 **db_owner**または**replmonitor**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [プログラムによるレプリケーションの監視](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
