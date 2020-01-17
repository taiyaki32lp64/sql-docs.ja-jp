---
title: sp_replmonitorhelppublisher (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5db934c972282609e9b2978a66034b39bb38a092
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771188"
---
# <a name="sp_replmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ディストリビューターに関連付けられている1つ以上のパブリッシャーの現在の状態情報を返します。 レプリケーションを監視するために使用されるこのストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`状態を監視するパブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値は NULL です。 NULL の場合、ディストリビューターを使用するすべてのパブリッシャーに関する情報が返されます。  
  
`[ @refreshpolicy = ] refreshpolicy`内部でのみ使用します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前です。|  
|**distribution_db**|**sysname**|特定のパブリッシャーによって使用されるディストリビューションデータベースの名前を指定します。|  
|**status**|**int**|このパブリッシャー側のパブリケーションに関連付けられているすべてのレプリケーション エージェントの最大の状態です。次のいずれかの値をとります。<br /><br /> **1** = 開始<br /><br /> **2** = 成功<br /><br /> **3** = 実行中<br /><br /> **4** = アイドル<br /><br /> **5** = 再試行中<br /><br /> **6** = 失敗|  
|**warning**|**int**|このパブリッシャーのパブリケーションに属するサブスクリプションによって生成される最大しきい値警告。これらの値の1つ以上の論理和になります。<br /><br /> **1** = 有効期限-トランザクションパブリケーションに対するサブスクリプションが、保有期間のしきい値内に同期されていません。<br /><br /> **2** = 待機時間-トランザクションパブリッシャーからサブスクライバーへのデータのレプリケートにかかった時間が、秒単位のしきい値を超えています。<br /><br /> **4** = mergeexpiration-マージパブリケーションに対するサブスクリプションが、保有期間のしきい値内に同期されていません。<br /><br /> **8** = mergefastrunduration-高速ネットワーク接続経由で、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **16** = mergeslowrunduration-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期の完了にかかった時間が、秒単位のしきい値を超えています。<br /><br /> **32** = mergefastrunspeed-高速ネットワーク接続上で、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でのしきい値の比率を維持できませんでした。<br /><br /> **64** = mergeslowrunspeed-低速またはダイヤルアップネットワーク接続を介して、マージサブスクリプションの同期中の行の配信率が、1秒あたりの行数でしきい値を維持できませんでした。|  
|**publicationcount**|**int**|パブリッシャーに属しているパブリケーションの数です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replmonitorhelppublisher**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replmonitorhelppublisher**を実行できるのは、ディストリビューター側の固定サーバーロール**sysadmin**のメンバー、またはディストリビューションデータベースの固定データベースロール**db_owner**または**replmonitor**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Programmatically Monitor Replication (プログラムによるレプリケーションの監視)](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
