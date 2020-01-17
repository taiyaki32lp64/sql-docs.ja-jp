---
title: sys.dm_db_objects_disabled_on_compatibility_level_change (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_objects_disabled_on_compatibility_level_change
- dm_db_objects_disabled_on_compatibility_level_change_TSQL
- sys.dm_db_objects_disabled_on_compatibility_level_change
- sys.dm_db_objects_disabled_on_compatibility_level_change_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_objects_disabled_on_compatibility_level_change catalog view
ms.assetid: a5d70064-0330-48b9-b853-01eba50755d0
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 30c3a5d7358e49c1e1762fbb9851066bdaf30871
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809905"
---
# <a name="spatial-data---sysdm_db_objects_disabled_on_compatibility_level_change"></a>空間データ-_db_objects_disabled_on_compatibility_level_change
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]互換性レベルを変更した結果として無効になるインデックスと制約の一覧を示します。 更新または互換性レベルの変更後に、式が空間 Udt を使用する、保存される計算列を含むインデックスおよび制約は無効になります。 互換性レベルの変更の影響を判断するには、この動的管理関数を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="Arguments"></a> 引数  
 *compatibility_level*  
 設定を計画している互換性レベルを識別する**int** 。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**class**|**int**|1 = 制約<br /><br /> 7 = インデックスとヒープ|  
|**class_desc**|**nvarchar(60)**|制約の場合は OBJECT または COLUMN<br /><br /> インデックスとヒープのインデックス|  
|**major_id**|**int**|制約の OBJECT ID<br /><br /> インデックスとヒープを含むテーブルのオブジェクト ID|  
|**minor_id**|**int**|制約の場合は NULL<br /><br /> インデックスとヒープの Index_id|  
|**dependency**|**nvarchar(60)**|制約またはインデックスが無効になる原因となっている依存関係の説明。 アップグレード中に発生した警告にも同じ値が使用されます。 具体的には次のものがあります。<br /><br /> 組み込み用の "space"<br /><br /> システム UDT の場合は "geometry"<br /><br /> システム UDT のメソッドの場合は "geography::Parse"|  
  
## <a name="general-remarks"></a>全般的な解説  
 互換性レベルを変更すると、一部の組み込み関数を使用している保存される計算列が無効になります。 データベースをアップグレードすると、Geometry メソッドまたは Geography メソッドを使用している保存される計算列も無効になります。  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>保存された計算列が無効になる関数を教えてください。  
 保存される計算列の式で次の関数を使用すると、互換性レベルが80から90に変更されたときに、これらの列を参照するインデックスと制約が無効になります。  
  
-   **IsNumeric**  
  
 保存される計算列の式で次の関数が使用されている場合、互換性レベルが 100 から 110 以上に変更されると、これらの列を参照するインデックスと制約が無効になります。  
  
-   **Soundex**  
  
-   **Geography::GeomFromGML**  
  
-   **Geography::STGeomFromText**  
  
-   **Geography::STLineFromText**  
  
-   **Geography::STPolyFromText**  
  
-   **Geography::STMPointFromText**  
  
-   **Geography::STMLineFromText**  
  
-   **Geography::STMPolyFromText**  
  
-   **Geography::STGeomCollFromText**  
  
-   **Geography::STGeomFromWKB**  
  
-   **Geography::STLineFromWKB**  
  
-   **Geography::STPolyFromWKB**  
  
-   **Geography::STMPointFromWKB**  
  
-   **Geography::STMLineFromWKB**  
  
-   **Geography::STMPolyFromWKB**  
  
-   **Geography::STUnion**  
  
-   **Geography::STIntersection**  
  
-   **Geography::STDifference**  
  
-   **Geography::STSymDifference**  
  
-   **Geography::STBuffer**  
  
-   **Geography::BufferWithTolerance**  
  
-   **Geography::分解**  
  
-   **Geography::落とし**  
  
### <a name="behavior-of-the-disabled-objects"></a>無効なオブジェクトの動作  
 **[インデックス]**  
  
 クラスター化インデックスが無効になっている場合、または非クラスター化インデックスが強制されている場合は、次のエラーが発生します。"インデックス '% のため、クエリプロセッサはプランを作成できません。\*ls ' テーブルまたはビュー '%。\*ls ' は無効になっています。 " これらのオブジェクトを再度有効にするには、アップグレード**後に ALTER INDEX ON...REBUILD** を使用して変更するときに選択できます。  
  
 **頻繁**  
  
 無効になったヒープが含まれているテーブルを使用すると、次のエラーが発生します。 これらのオブジェクトを再度有効にするには、アップグレード**後に ALTER INDEX ALL を呼び出すことによって再構築します...REBUILD** を使用して変更するときに選択できます。  
  
```  
// ErrorNumber: 8674  
// ErrorSeverity: EX_USER  
// ErrorFormat: The query processor is unable to produce a plan because the table or view '%.*ls' is disabled.  
// ErrorCause: The table has a disabled heap.   
// ErrorCorrectiveAction: Rebuild the disabled heap to enable it.   
// ErrorInserts: table or view name   
// ErrorOwner: mtintor   
// ErrorFirstProduct: SQL11  
```  
  
 オンライン操作中にヒープを再構築しようとすると、エラーが発生します。  
  
 **Check 制約と外部キー**  
  
 無効になっている check 制約と外部キーでは、エラーは発生しません。 ただし、行が変更されても、制約は適用されません。 これらのオブジェクトを再度有効にするには、アップグレード後に**ALTER TABLE... を呼び出して、制約を確認します。CHECK 制約**。  
  
 **保存される計算列**  
  
 1 つの列を無効にすることはできないので、クラスター化インデックスまたはヒープを無効にすると、テーブル全体が無効になります。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 VIEW DATABASE STATE 権限が必要です。  
  
## <a name="example"></a>例  
 次の例では、互換性レベルを120に変更することによって影響を受けるオブジェクトを検索するための、 **_db_objects_disabled_on_compatibility_level_change**に対するクエリを示します。  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
