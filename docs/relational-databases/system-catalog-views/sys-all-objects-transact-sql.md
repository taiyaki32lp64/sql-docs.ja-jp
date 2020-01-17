---
title: sys.all_objects (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.all_objects
- all_objects_TSQL
- all_objects
- sys.all_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_objects catalog view
ms.assetid: 547e4be4-a8e4-48ce-9d8d-37b169985081
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 499b1ddeeafbc21a923f15102a67d9c0a332f069
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018160"
---
# <a name="sysallobjects-transact-sql"></a>sys.all_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  すべてのスキーマ スコープ ユーザー定義オブジェクトおよびシステム オブジェクトの和集合を示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|オブジェクト名です。|  
|object_id|**int**|オブジェクト ID 番号。 データベース内で一意です。|  
|principal_id|**int**|スキーマの所有者と異なる場合は、個々 の所有者の ID。 既定では、スキーマに含まれるオブジェクトは、スキーマの所有者によって所有されます。 ただし、別の所有者は所有権を変更する ALTER AUTHORIZATION ステートメントを使用して指定できます。<br /><br /> 代替の所有者がない場合は NULL です。<br /><br /> オブジェクトの型が次のいずれかの場合は NULL になります。<br /><br /> C = CHECK 制約<br /><br /> D = DEFAULT (制約またはスタンドアロン)<br /><br /> F = FOREIGN KEY 制約<br /><br /> PK = PRIMARY KEY 制約<br /><br /> R = ルール (旧形式、スタンドアロン)<br /><br /> TA = アセンブリ (CLR) トリガー<br /><br /> TR = SQL トリガー<br /><br /> UQ = UNIQUE 制約|  
|schema_id|**int**|オブジェクトを含むスキーマの ID。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に含まれるすべてのスキーマ スコープ システム オブジェクトに対して、この値は常に (schema_id('sys'), schema_id('INFORMATION_SCHEMA')) の形式で示されます。|  
|parent_object_id|**int**|このオブジェクトが所属するオブジェクトの ID。<br /><br /> 0 = 子オブジェクトではありません。|  
|type|**char(2)**|オブジェクトの種類:<br /><br /> AF = 集計関数 (CLR)<br /><br /> C = CHECK 制約<br /><br /> D = DEFAULT (制約またはスタンドアロン)<br /><br /> F = FOREIGN KEY 制約<br /><br /> FN = SQL スカラー関数<br /><br /> FS = アセンブリ (CLR) スカラー関数<br /><br /> FT = アセンブリ (CLR) テーブル値関数<br /><br /> IF = SQL インライン テーブル値関数<br /><br /> IT = 内部テーブル<br /><br /> P = SQL ストアド プロシージャ<br /><br /> PC = アセンブリ (CLR) ストアド プロシージャ<br /><br /> PG = プラン ガイド<br /><br /> PK = PRIMARY KEY 制約<br /><br /> R = ルール (旧形式、スタンドアロン)<br /><br /> RF = レプリケーション フィルター プロシージャ<br /><br /> S = システム ベース テーブル<br /><br /> SN = シノニム<br /><br /> SQ = サービス キュー<br /><br /> TA = アセンブリ (CLR) DML トリガー<br /><br /> TF = SQL テーブル値関数<br /><br /> TR = SQL DML トリガー<br /><br /> TT = テーブル型<br /><br /> U = テーブル (ユーザー定義)<br /><br /> UQ = UNIQUE 制約<br /><br /> V = ビュー<br /><br /> X = 拡張ストアド プロシージャ|  
|type_desc|**nvarchar(60)**|オブジェクトの種類の説明です。 AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> DEFAULT_CONSTRAINT<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> INTERNAL_TABLE<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> RULE<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> SYSTEM_TABLE<br /><br /> SYNONYM<br /><br /> SERVICE_QUEUE<br /><br /> CLR_TRIGGER<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> TABLE_TYPE<br /><br /> USER_TABLE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> VIEW<br /><br /> EXTENDED_STORED_PROCEDURE|  
|create_date|**datetime**|オブジェクトが作成された日付です。|  
|modify_date|**datetime**|ALTER ステートメントを使用して、オブジェクトの最終更新日。 オブジェクトがテーブルまたはビューの場合は、modify_date は、テーブルまたはビューのクラスター化インデックスを作成または変更時にも変更されます。|  
|is_ms_shipped|**bit**|内部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントによって作成されたオブジェクトです。|  
|is_published|**bit**|オブジェクトが発行されます。|  
|is_schema_published|**bit**|オブジェクトのスキーマのみがパブリッシュされることを示します。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.system_objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)  
  
  
