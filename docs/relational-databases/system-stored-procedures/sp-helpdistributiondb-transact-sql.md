---
title: sp_helpdistributiondb (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 90dee1076743ae54201248c808b04c6197d42198
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770930"
---
# <a name="sp_helpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定されたディストリビューションデータベースのプロパティを返します。 このストアド プロシージャは、ディストリビューター側でディストリビューション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @database = ] 'database_name'`プロパティを返すデータベース名を指定します。 *database_name*は**sysname**,、既定値 **%** は、ディストリビューターに関連付けられているすべてのデータベースに対して、ユーザーが権限を持っています。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|ディストリビューションデータベースの名前。|  
|**min_distretention**|**int**|トランザクションが削除されるまでの最小保有期間 (時間単位)。|  
|**max_distretention**|**int**|トランザクションが削除されるまでの最大保有期間 (時間単位)。|  
|**history retention**|**int**|履歴を保持する時間数。|  
|**history_cleanup_agent**|**sysname**|履歴クリーンアップエージェントの名前。|  
|**distribution_cleanup_agent**|**sysname**|ディストリビューションクリーンアップエージェントの名前。|  
|**status**|**int**|内部使用のみです。|  
|**data_folder**|**nvarchar (255)**|データベース ファイルを格納するときに使用するディレクトリの名前。|  
|**data_file**|**nvarchar (255)**|データベースファイルの名前。|  
|**data_file_size**|**int**|データ ファイルの初期サイズ (MB 単位)。|  
|**log_folder**|**nvarchar (255)**|データベース ログ ファイルを格納するディレクトリの名前。|  
|**log_file**|**nvarchar (255)**|ログファイルの名前。|  
|**log_file_size**|**int**|ログファイルの初期サイズ (mb 単位)。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpdistributiondb**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 ディストリビューションデータベースの**db_owner**固定データベースロールのメンバー、またはディストリビューションデータベースの**replmonitor**ロールのメンバー、およびディストリビューションデータベースを使用するパブリケーションのパブリケーションアクセスリストのユーザーは、 **sp_helpdistributiondb**を実行してを返すことができます。ファイルに関連する情報。 **Public**ロールのメンバーは、 **sp_helpdistributiondb**を実行して、アクセス権のあるディストリビューションデータベースについて、ファイルに関連しない情報を返すことができます。  
  
## <a name="see-also"></a>関連項目  
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
