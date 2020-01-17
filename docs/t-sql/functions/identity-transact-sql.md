---
title: '@@IDENTITY (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@IDENTITY_TSQL'
- '@@IDENTITY'
dev_langs:
- TSQL
helpviewer_keywords:
- last-inserted identity values
- identity values [SQL Server], last-inserted
- '@@IDENTITY function'
ms.assetid: 912e4485-683c-41c2-97b3-8831c0289ee4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e1b4177de655300e8297d450ab382c6f37a9f0fe
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843655"
---
# <a name="x40x40identity-transact-sql"></a>&#x40;&#x40;IDENTITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  最後に挿入された ID 値を返すシステム関数です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
@@IDENTITY  
```  
  
## <a name="return-types"></a>戻り値の型  
 **numeric(38,0)**  
  
## <a name="remarks"></a>Remarks  
 INSERT ステートメント、SELECT INTO ステートメント、または一括コピーが終了すると、@@IDENTITY にはステートメントが最後に生成した ID 値が含まれます。 ID 列のあるテーブルがステートメントによって影響されなかった場合、@@IDENTITY は NULL 値を返します。 複数の行を挿入して、複数の ID 値を生成する場合、@@IDENTITY は最後に生成した ID 値を返します。 ステートメントが、ID 値を生成する挿入操作を実行する 1 つ以上のトリガーを起動する場合、このステートメントの直後で @@IDENTITY を呼び出すと、トリガーにより最後に生成された ID 値が返されます。 ID 列のあるテーブルで挿入操作を行った後に起動されるトリガーによって、ID 列のない別のテーブルへの挿入操作が実行される場合、@@IDENTITY は最初の挿入の ID 値を返します。 INSERT ステートメントか SELECT INTO ステートメント、または一括コピーが失敗した場合、あるいは、トランザクションがロールバックされた場合、@@IDENTITY 値は前の設定に戻りません。  
  
 失敗したステートメントとトランザクションによって、テーブルに対する現在の ID が変更され、ID 列値に差異が生じる可能性があります。 ID 値がロールバックされることはありません。これは、テーブルに値を挿入するトランザクションがコミットされない場合でも同じです。 たとえば、INSERT ステートメントが IGNORE_DUP_KEY 違反のために失敗しても、テーブルの現在の ID 値は増分されます。  
  
 @@IDENTITY、SCOPE_IDENTITY、および IDENT_CURRENT は、すべてテーブルの IDENTITY 列に最後に挿入された値を返すという点で似ています。  
  
 @@IDENTITY と SCOPE_IDENTITY は、現在のセッション内の任意のテーブルで生成された最後の ID 値を返します。 ただし、SCOPE_IDENTITY が返す値は、現在のスコープの範囲内に限られます。@@IDENTITY の場合は、特定のスコープに限定されません。  
  
 IDENT_CURRENT はスコープとセッションには限定されませんが、特定のテーブルに限定されます。 IDENT_CURRENT は、任意のセッションおよび任意のスコープ内の特定のテーブルに対して生成された ID 値を返します。 詳しくは、「[IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)」をご覧ください。  
  
 @@IDENTITY 関数のスコープは、実行されるローカル サーバーの現在のセッションです。 この関数は、リモート サーバーまたはリンク サーバーには適用できません。 別のサーバーで ID 値を取得するには、そのリモート サーバーまたはリンク サーバーでストアド プロシージャを実行し、(リモート サーバーまたはリンク サーバーのコンテキスト内で実行されている) そのストアド プロシージャが ID 値を収集し、ローカル サーバー上の呼び出し元の接続にこれを返すようにします。  
  
 @@IDENTITY の値はレプリケーション トリガーやストアド プロシージャ内で使用されるため、レプリケーションによって影響を受けることがあります。 列がレプリケーション アーティクルの一部である場合、ユーザーが作成した最新の ID として @@IDENTITY を信頼することはできません。 @@IDENTITY の代わりに、SCOPE_IDENTITY() 関数の構文を使用できます。 詳細については、「[SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  呼び出し元のストアド プロシージャまたは [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、そのユーザーのステートメントのスコープ内で使用される最新の id と、レプリケーションで使用する入れ子になったトリガーのスコープ内での id ではなく返す `SCOPE_IDENTITY()` 関数を使用して書き直す必要があります。  
  
## <a name="examples"></a>使用例  
 次の例では、ID 列 (`LocationID`) のあるテーブルに行を挿入し、`@@IDENTITY` を使用して新しい行で使用する ID 値を表示します。  
  
```  
USE AdventureWorks2012;  
GO  
--Display the value of LocationID in the last row in the table.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
INSERT INTO Production.Location (Name, CostRate, Availability, ModifiedDate)  
VALUES ('Damaged Goods', 5, 2.5, GETDATE());  
GO  
SELECT @@IDENTITY AS 'Identity';  
GO  
--Display the value of LocationID of the newly inserted row.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
