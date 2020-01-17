---
title: sys.sysobjects (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysobjects_TSQL
- sysobjects
- sysobjects_TSQL
- sys.sysobjects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysobjects compatibility view
- sysobjects system table
ms.assetid: 44fdc387-67b0-4139-8bf5-ed26cf640cd1
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26d4860c7ea434aecb0255134178b73fb7c01be4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995606"
---
# <a name="syssysobjects-transact-sql"></a>sys.sysobjects (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  制約、デフォルト、ログ、ルール、ストアド プロシージャなど、データベース内で作成されるオブジェクトごとに 1 行のデータを保持します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|オブジェクト名です。|  
|id|**int**|オブジェクト id 番号|  
|xtype|**char(2)**|オブジェクトの種類です。 次のオブジェクトの種類のいずれかを指定できます。<br /><br /> AF = 集計関数 (CLR)<br /><br /> C = CHECK 制約<br /><br /> D = 既定値または既定の制約<br /><br /> F = FOREIGN KEY 制約<br /><br /> L = ログ<br /><br /> FN = スカラー関数<br /><br /> FS = アセンブリ (CLR) スカラー関数<br /><br /> FT = アセンブリ (CLR) テーブル値関数<br /><br /> IF = インライン テーブル関数<br /><br /> IT = 内部テーブル<br /><br /> P = ストアド プロシージャ<br /><br /> PC = アセンブリ (CLR) ストアド プロシージャ<br /><br /> PK = PRIMARY KEY 制約 (種類は K)<br /><br /> RF = レプリケーション フィルター ストアド プロシージャ<br /><br /> S = システム テーブル<br /><br /> SN = シノニム<br /><br /> SQ = サービス キュー<br /><br /> TA = アセンブリ (CLR) DML トリガー<br /><br /> TF = テーブル関数<br /><br /> TR = SQL DML トリガー<br /><br /> TT = テーブル型<br /><br /> U = ユーザー テーブル<br /><br /> UQ = UNIQUE 制約 (種類は K)<br /><br /> V = ビュー<br /><br /> X = 拡張ストアド プロシージャ|  
|uid|**smallint**|オブジェクトの所有者のスキーマ ID です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の前のバージョンからアップグレードしたデータベースの場合、スキーマ ID は所有者のユーザー ID と同じです。 オーバーフローまたはユーザーおよびロールの数が 32,767 を超える場合は NULL を返します。<br /><br /> **\*\* 重要な\* \*** 場合は、次のいずれかを使用する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、DDL ステートメントを使用する必要がある、 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)カタログ sys.sysobjects ではなくビュー。<br /><br /> 作成&#124;ALTER&#124;ドロップ ユーザー<br /><br /> 作成&#124;ALTER&#124;ドロップ ロール<br /><br /> 作成&#124;ALTER &#124; DROP APPLICATION ROLE<br /><br /> CREATE SCHEMA<br /><br /> ALTER AUTHORIZATION ON OBJECT|  
|info|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|base_schema_ver|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|replinfo|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|parent_obj|**int**|親オブジェクトのオブジェクト id 番号。 たとえば、トリガーや制約の場合はテーブル ID です。|  
|crdate|**datetime**|オブジェクトが作成された日付です。|  
|ftcatid|**smallint**|フルテキスト インデックス作成で登録されたすべてのユーザー テーブルのフルテキスト カタログの識別子です。登録されていないすべてのユーザー テーブルには 0 を指定します。|  
|schema_ver|**int**|テーブルのスキーマが変更されるたびに増加するバージョン番号です。 常に 0 を返します。|  
|stats_schema_ver|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|type|**char(2)**|オブジェクトの種類です。 次の値のいずれかです。<br /><br /> AF = 集計関数 (CLR)<br /><br /> C = CHECK 制約<br /><br /> D = 既定値または既定の制約<br /><br /> F = FOREIGN KEY 制約<br /><br /> FN = スカラー関数<br /><br /> FS = アセンブリ (CLR) スカラー関数<br /><br /> FT = アセンブリ (CLR) テーブル値関数 If = インライン テーブル関数<br /><br /> IT = 内部テーブル<br /><br /> K = PRIMARY KEY または UNIQUE 制約<br /><br /> L = ログ<br /><br /> P = ストアド プロシージャ<br /><br /> PC = アセンブリ (CLR) ストアド プロシージャ<br /><br /> R = ルール<br /><br /> RF = レプリケーション フィルター ストアド プロシージャ<br /><br /> S = システム テーブル<br /><br /> SN = シノニム<br /><br /> SQ = サービス キュー<br /><br /> TA = アセンブリ (CLR) DML トリガー<br /><br /> TF = テーブル関数<br /><br /> TR = SQL DML トリガー<br /><br /> TT = テーブル型<br /><br /> U = ユーザー テーブル<br /><br /> V = ビュー<br /><br /> X = 拡張ストアド プロシージャ|  
|userstat|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|sysstat|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|indexdel|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|refdate|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|version|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|deltrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|instrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|updtrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|seltrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|カテゴリ|**int**|パブリケーション、制約、および id に使用されます。|  
|キャッシュ|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
