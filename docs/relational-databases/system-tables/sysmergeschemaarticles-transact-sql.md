---
title: sysmergeschemaarticles (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9446d03db98d7fa5181fb0217814cdd86c55de1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029813"
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ レプリケーションのスキーマだけのアーティクルを追跡します。 このテーブルは、パブリケーション データベースとサブスクリプション データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|マージ パブリケーションでスキーマだけのアーティクルの名前。|  
|**type**|**tinyint**|次のいずれかのスキーマだけのアーティクルの種類を示します。<br /><br /> **0x20**ストアド プロシージャのスキーマだけのアーティクルを = です。<br /><br /> **0x40** = ビュー スキーマのみのアーティクルまたはインデックス付きビュー スキーマのみのアーティクルです。|  
|**objid**|**int**|アーティクルのベース オブジェクトのオブジェクト識別子です。 プロシージャ、ビュー、インデックス、ビュー、またはユーザー定義関数のオブジェクト識別子を指定できます。|  
|**artid**|**uniqueidentifier**|アーティクルの id。|  
|**description**|**nvarchar (255)**|この記事の説明です。|  
|**pre_creation_command**|**tinyint**|サブスクリプション データベースの中でアーティクルが作成されるときに実行される既定の操作。<br /><br /> **0 =** なし - サブスクライバーで、テーブルが既に存在する場合操作はありません。<br /><br /> **1** = drop - テーブルを再作成する前に削除します。<br /><br /> **2** = 削除-サブセット フィルターの WHERE 句に基づいて削除します。<br /><br /> **3** = Truncate のと同じ**2**が行ではなくページを削除します。 ただし、WHERE 句は使用しません。|  
|**pubid**|**uniqueidentifier**|パブリケーションの一意の識別子。|  
|**status**|**tinyint**|スキーマだけのアーティクルの状態。次のいずれかになります。<br /><br /> **1** = Unsynced - テーブルに、次回、スナップショット エージェントの実行をパブリッシュする初期処理スクリプト。<br /><br /> **2** = active - テーブルをパブリッシュする初期処理スクリプトが実行されています。<br /><br /> **5** = New_inactive - 追加します。<br /><br /> **6** = New_active - 追加します。|  
|**creation_script**|**nvarchar (255)**|ターゲット テーブルの作成に使用されるアーティクル スキーマの事前作成スクリプトのパスと名前 (省略可能)。|  
|**schema_option**|**binary(8)**|スキーマだけのアーティクルに関連するスキーマ生成オプションのビットマップ。次の値のうち 1 つ以上の結果を、ビットごとに論理和演算したものになります。<br /><br /> **0x00** = スナップショット エージェントによるスクリプト作成を無効にしては、指定されたいる creationscript を使用します。<br /><br /> **0x01** = オブジェクトの作成 (CREATE TABLE、CREATE PROCEDURE など) を生成します。<br /><br /> **0x10** = 対応するクラスター化インデックスを生成します。<br /><br /> **0x20** = ユーザー定義データ型を基本データ型に変換します。<br /><br /> **0x40** = 対応する非クラスター化インデックスを生成またはインデックスです。<br /><br /> **0x80** Include の主キーに関する宣言参照整合性を = です。<br /><br /> **0x100**定義されている場合、テーブル アーティクル上のレプリケートのユーザー トリガーを = です。<br /><br /> **0x200** = 外部キー制約をレプリケートします。 参照先のテーブルがパブリケーションの一部は、パブリッシュされたテーブルですべての外部キー制約はレプリケートされません。<br /><br /> **0x400** = check 制約をレプリケートします。<br /><br /> **0x800** = 既定値をレプリケートします。<br /><br /> **0x1000** = 列レベルの照合順序をレプリケートします。<br /><br /> **0x2000** = 拡張パブリッシュされるアーティクルのソース オブジェクトに関連付けられたプロパティをレプリケートします。<br /><br /> **0x4000** = テーブル アーティクルで定義されている場合、一意なキーをレプリケートします。<br /><br /> **0x8000** = ALTER TABLE ステートメントを使用して、制約として主キーと、テーブルの一意のキーの記事をレプリケートします。<br /><br /> 指定できる値の詳細については**schema_option**を参照してください[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)します。|  
|**destination_object**|**sysname**|サブスクリプション データベース内の変換先オブジェクトの名前。 この値は、ストアド プロシージャ、ビュー、Udf などのスキーマだけのアーティクルにのみ適用されます。|  
|**destination_owner**|**sysname**|ない場合、サブスクリプション データベース内のオブジェクトの所有者**dbo**します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
