---
title: sysschemaarticles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysschemaarticles_TSQL
- sysschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysschemaarticles system table
ms.assetid: 67a1c039-c283-4a9c-bacc-b9b3973590c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7bd511eb6eeff5cd412504373e7214703c845cd0
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811341"
---
# <a name="sysschemaarticles-transact-sql"></a>sysschemaarticles (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トランザクションパブリケーションおよびスナップショットパブリケーションのスキーマのみのアーティクルを追跡します。 このテーブルは、パブリケーション データベース内に保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|アーティクル ID です。|  
|**creation_script**|**nvarchar (255)**|ターゲット テーブルを作成するのに使用されるアーティクル スキーマのスクリプトのパスと名前です。|  
|**description**|**nvarchar (255)**|アーティクルの説明エントリです。|  
|**dest_object**|**sysname**|アーティクルがストアド プロシージャ、ビュー、UDF など、スキーマだけのアーティクルの場合は、サブスクリプション データベースのオブジェクト名です。|  
|**name**|**sysname**|パブリケーション内のスキーマのみのアーティクルの名前です。|  
|**objid**|**int**|アーティクルベースオブジェクトのオブジェクト識別子。 プロシージャ、ビュー、インデックス付き、ビュー、または UDF のオブジェクト識別子を指定できます。|  
|**pubid**|**int**|パブリケーションの ID です。|  
|**pre_creation_cmd**|**tinyint**|このアーティクルのスナップショットを適用するときに、サブスクライバーで同じ名前の既存のオブジェクトが検出された場合にシステムが実行する操作を指定します。<br /><br /> **0** = Nothing。<br /><br /> **1** = ターゲットテーブルを削除します。<br /><br /> **2** = ターゲットテーブルを削除します。<br /><br /> **3** = 変換先テーブルを切り捨てます。|  
|**status**|**int**|アーティクルの状態を示すために使用するビットマップ。|  
|**type**|**tinyint**|スキーマだけのアーティクルの種類を示す値です。<br /><br /> **32** = ストアドプロシージャ。<br /><br /> **64** = ビューまたはインデックス付きビュー。 <br /><br /> **96** = 集計関数。<br /><br /> **128** = 関数。|  
|**schema_option**|**binary(8)**|指定されたアーティクルのスキーマ生成オプションのビットマスク。 すべての CALL/MCALL/XCALL 構文の目的のデータベース内での、ストアド プロシージャの自動作成を指定します。次の値 (1 つまたは複数) のビットごとの論理和となります。<br /><br /> **0x00** = スナップショットエージェントによるスクリプト作成を無効にし、 *creation_script*を使用します。<br /><br /> **0x01** = オブジェクトの作成 (CREATE TABLE、CREATE PROCEDURE など) を生成します。 この値は、ストアドプロシージャアーティクルの既定値です。<br /><br /> **0x02** = 定義されている場合、アーティクルのカスタムストアドプロシージャを生成します。<br /><br /> **0x10** = 対応するクラスター化インデックスを生成します。<br /><br /> **0x20** = ユーザー定義データ型を基本データ型に変換します。<br /><br /> **0x40**= 対応する非クラスター化インデックスを生成します。<br /><br /> **0x80**= 宣言された参照整合性を主キーに含めます。<br /><br /> **0x73** = CREATE TABLE ステートメントを生成し、クラスター化インデックスと非クラスター化インデックスを作成し、ユーザー定義データ型を基本データ型に変換し、サブスクライバーで適用されるカスタムストアドプロシージャスクリプトを生成します。 ストアド プロシージャ アーティクル以外のすべてのアーティクルの既定値です。<br /><br /> **0x100**= 定義されている場合、テーブルアーティクル上のユーザートリガーをレプリケートします。<br /><br /> **0x200**= 外部キー制約をレプリケートします。 参照先のテーブルがパブリケーションの一部でない場合、パブリッシュされたテーブルのすべての foreign key 制約はレプリケートされません。<br /><br /> **0x400**= check 制約をレプリケートします。<br /><br /> **0x800**= 既定値をレプリケートします。<br /><br /> **0x1000**= 列レベルの照合順序をレプリケートします。<br /><br /> **0x2000**= パブリッシュされたアーティクルのソースオブジェクトに関連付けられた拡張プロパティをレプリケートします。<br /><br /> **0x4000**= テーブルアーティクルで定義されている場合、一意キーをレプリケートします。<br /><br /> **0x8000**= ALTER table ステートメントを使用して、テーブルアーティクル上の主キーと一意キーを制約としてレプリケートします。|  
|**dest_owner**|**sysname**|目的のデータベースにおけるテーブルの所有者です。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
