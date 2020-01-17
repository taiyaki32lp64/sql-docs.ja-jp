---
title: sys.fn_validate_plan_guide (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_validate_plan_guide
- sys.fn_validate_plan_guide_TSQL
- fn_validate_plan_guide
- fn_validate_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_validate_plan_guide function
- sys.fn_validate_plan_guide function
ms.assetid: 3af8b47a-936d-4411-91d1-d2d16dda5623
author: rothja
ms.author: jroth
ms.openlocfilehash: a76835272ed86faeab807f97f6e8801985062733
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059188"
---
# <a name="sysfnvalidateplanguide-transact-sql"></a>sys.fn_validate_plan_guide (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したプラン ガイドの有効性を確認します。 sys.fn_validate_plan_guide 関数では、クエリにプラン ガイドを適用した場合に最初に発生するエラーのメッセージが返されます。 プラン ガイドが有効な場合は空の行セットが返されます。 データベースの物理デザインに変更を行った後、プラン ガイドが無効になることができます。 たとえば、プラン ガイドでは、特定のインデックスとそのインデックスが削除される、その後を指定する場合、クエリできなくプラン ガイドを使用することです。  
  
 プラン ガイドを検証することで、変更を加えずにオプティマイザーで使用できるかどうかを確認できます。 この関数の結果に基づいて、そのプラン ガイドを削除してクエリを再チューニングするか、データベースのデザインを変更する (プラン ガイドで指定されているインデックスを再作成するなど) かを決定できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.fn_validate_plan_guide ( plan_guide_id )  
```  
  
## <a name="arguments"></a>引数  
 *plan_guide_id*  
 報告されるプラン ガイドの ID は、 [sys.plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)カタログ ビューです。 *plan_guide_id*は**int**既定値はありません。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|msgnum|**int**|エラー メッセージの ID です。|  
|重要度|**tinyint**|メッセージの重大度レベルです。有効値は 1 ～ 25 です。|  
|state|**smallint**|エラーが発生したコード内の場所を示すエラーの状態番号です。|  
|メッセージ|**nvarchar(2048)**|エラー メッセージのテキストです。|  
  
## <a name="permissions"></a>アクセス許可  
 スコープが OBJECT のプラン ガイドでは、参照先オブジェクトに対する VIEW DEFINITION 権限または ALTER 権限と、プラン ガイドに含まれるクエリやバッチをコンパイルするための権限が必要です。 たとえば、バッチに SELECT ステートメントが含まれている場合は、参照先オブジェクトに対する SELECT 権限が必要です。  
  
 スコープが SQL または TEMPLATE のプラン ガイドでは、データベースに対する ALTER 権限と、プラン ガイドに含まれるクエリやバッチをコンパイルするための権限が必要です。 たとえば、バッチに SELECT ステートメントが含まれている場合は、参照先オブジェクトに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-validating-all-plan-guides-in-a-database"></a>A. データベースのすべてのプラン ガイドの検証をテストする  
 次の例では、現在のデータベースのすべてのプラン ガイドの有効性を確認します。 空の結果セットが返された場合は、すべてのプラン ガイドが有効です。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT plan_guide_id, msgnum, severity, state, message  
FROM sys.plan_guides  
CROSS APPLY fn_validate_plan_guide(plan_guide_id);  
GO  
```  
  
### <a name="b-testing-plan-guide-validation-before-implementing-a-change-to-the-database"></a>B. データベースに変更を実装する前にプラン ガイドの検証のテスト  
 次の例では、インデックスを削除する明示的なトランザクションを使用します。 `sys.fn_validate_plan_guide`このアクションで、データベース内のすべてのプラン ガイドを無効にするかどうかを判断する関数を実行します。 この関数の結果に基づいて、`DROP INDEX` ステートメントがコミットされるか、トランザクションがロールバックされます。トランザクションがロールバックされた場合は、インデックスは削除されません。  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DROP INDEX IX_SalesOrderHeader_CustomerID ON Sales.SalesOrderHeader;  
-- Check for invalid plan guides.  
IF EXISTS (SELECT plan_guide_id, msgnum, severity, state, message  
           FROM sys.plan_guides  
           CROSS APPLY sys.fn_validate_plan_guide(plan_guide_id))  
    ROLLBACK TRANSACTION;  
ELSE  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [プラン ガイド](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
