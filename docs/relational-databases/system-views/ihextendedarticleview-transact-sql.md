---
title: IHextendedArticleView (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0abca8ca826ec986a9cbf71f4fb577291e095e39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029545"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHextendedArticleView**ビューは、SQL Server 以外のパブリケーションでアーティクルに関する情報を公開します。 このビューは、**distribution**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|発行者の一意の識別子。|  
|**publication_id**|**int**|パブリケーションの一意の識別子。|  
|**article**|**sysname**|アーティクルの名前|  
|**destination_object**|**sysname**|サブスクライバー側でパブリッシュされたオブジェクトの名前。|  
|**source_owner**|**sysname**|パブリッシャー側でパブリッシュされたオブジェクトの所有者です。|  
|**source_object**|**sysname**|パブリッシャー側でパブリッシュされたオブジェクトの名前。|  
|**description**|**nvarchar (255)**|この記事の説明です。|  
|**creation_script**|**nvarchar (255)**|そのアーティクルのスキーマ作成スクリプトです。|  
|**del_cmd**|**nvarchar (255)**|DELETE に対して実行されるコマンドです。|  
|**filter**|**int**|行方向のパーティション分割を定義するために使用するストアド プロシージャの識別子です。|  
|**filter_clause**|**ntext**|アーティクルを行方向にフィルター選択するために使用する WHERE 句です。|  
|**ins_cmd**|**nvarchar (255)**|INSERT に対して実行されるコマンドです。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE、または TRUNCATE 事前作成コマンド:<br /><br /> **0** = none。<br /><br /> **1** = ドロップします。<br /><br /> **2** = 削除します。<br /><br /> **3** = TRUNCATE です。|  
|**status**|**tinyint**|アーティクル オプションとステータスのビットマスクです。次に示す 1 つ以上の値のビットごとの論理和演算をとります。<br /><br /> **1** = アーティクルはアクティブです。<br /><br /> **8** = INSERT ステートメントに列名を含みます。<br /><br /> **16** = ステートメントをパラメーター化を使用します。<br /><br /> **24** = INSERT ステートメントに列名は、どちらも、パラメーター化されたステートメントを使用しています。<br /><br /> たとえば、パラメーター化されたステートメントを使用するアクティブなアーティクルの値があります**17**この列にします。 値**0**アーティクルがアクティブでないと、追加のプロパティが定義されていないことを意味します。|  
|**type**|**tinyint**|アーティクルの種類。<br /><br /> **1**ログベースのアーティクルを = です。<br /><br /> **3** = 手動フィルター付きログベースのアーティクルです。<br /><br /> **5** = 手動ビュー付きログベースのアーティクルです。<br /><br /> **7** = 手動フィルターおよび手動ビュー付きログベースのアーティクルです。|  
|**upd_cmd**|**nvarchar (255)**|このコマンドは、更新プログラムの実行です。|  
|**schema_option**|**nary**|新機能をスクリプト化することを示します。参照してください[sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)サポートされるスキーマ オプションの一覧についてはします。|  
|**dest_owner**|**sysname**|転送先データベースでパブリッシュされたオブジェクトの所有者です。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
