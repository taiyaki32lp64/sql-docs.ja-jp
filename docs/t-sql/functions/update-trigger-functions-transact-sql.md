---
title: UPDATE() (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATE()_TSQL
- UPDATE()
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], UPDATE function
- testing column updates
- UPDATE function
- UPDATE() function
- detecting changes
- columns [SQL Server], change detection
- UPDATE statement [SQL Server], UPDATE function
- verifying column updates
- checking column updates
ms.assetid: 8e3be25b-2e3b-4d1f-a610-dcbbd8d72084
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fefd85737e5d58e71dae6fd81dc2c0306b0838e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927630"
---
# <a name="update---trigger-functions-transact-sql"></a>UPDATE - トリガー関数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  テーブルまたはビューの指定された列で、INSERT または UPDATE が行われたかどうかを示すブール値を返します。 UPDATE() は [!INCLUDE[tsql](../../includes/tsql-md.md)] の INSERT または UPDATE トリガーの内部のどこでも使用でき、そのトリガーが特定の動作を実行すべきかどうかをテストすることができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
  
UPDATE ( column )   
```  
  
## <a name="arguments"></a>引数  
 *column*  
 INSERT 動作または UPDATE 動作をテストする列の名前です。 トリガーの ON 句にテーブル名が指定されているため、列名の前にテーブル名を含めないでください。 この列の[データ型](../../t-sql/data-types/data-types-transact-sql.md)は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がサポートしているものであれば、どのようなデータ型でもかまいません。 ただし、計算列を使用することはできません。  
  
## <a name="return-types"></a>戻り値の型  
 Boolean  
  
## <a name="remarks"></a>Remarks  
 INSERT または UPDATE が成功するかどうかにかかわらず、UPDATE() は TRUE を返します。  
  
 複数の列で INSERT 動作または UPDATE 動作をテストするには、最初の UPDATE(*column*) 句に続けて、別の UPDATE(column) 句を指定します。 COLUMNS_UPDATED を使用しても、複数の列で INSERT 動作または UPDATE 動作をテストできます。 これは、挿入または更新された列を示すビット パターンを返します。  
  
 INSERT 動作では、列には明示的な値または暗黙的な (NULL) 値が挿入されるので、IF UPDATE は TRUE の値を返します。  
  
> [!NOTE]  
>  IF UPDATE(*column*) 句は、IF 句、IF...ELSE 句、または WHILE 句と同じように機能し、BEGIN...END ブロックを使用できます。 詳細については、「[フロー制御言語](~/t-sql/language-elements/control-of-flow.md)」を参照してください。  
  
 UPDATE(*column*) は、[!INCLUDE[tsql](../../includes/tsql-md.md)] トリガーの内部のどこでも使用できます。  
 
トリガーを列に適用すると、列の値が更されない場合でも、`UPDATED` 値が `true` または `1` として返されます。 これは意図されたもので、トリガーでは挿入/更新/削除操作を許容するかどうかを決定するビジネス ロジックを実装する必要があります。 
  
## <a name="examples"></a>使用例  
 次の例では、`StateProvinceID` テーブルの `PostalCode` 列または `Address` 列を更新しようとするときにクライアントへのメッセージを出力する、トリガーを作成します。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
      WHERE name = 'reminder' AND type = 'TR')  
   DROP TRIGGER Person.reminder;  
GO  
CREATE TRIGGER reminder  
ON Person.Address  
AFTER UPDATE   
AS   
IF ( UPDATE (StateProvinceID) OR UPDATE (PostalCode) )  
BEGIN  
RAISERROR (50009, 16, 10)  
END;  
GO  
-- Test the trigger.  
UPDATE Person.Address  
SET PostalCode = 99999  
WHERE PostalCode = '12345';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
