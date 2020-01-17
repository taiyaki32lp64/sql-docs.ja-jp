---
title: CREATE DEFAULT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_DEFAULT_TSQL
- CREATE DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], default
- default objects
- CREATE DEFAULT statement
- objects [SQL Server], creating
- DEFAULT definition
ms.assetid: 08475db4-7d90-486a-814c-01a99d783d41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0d6b786725dfb50fceb1376fd104a4b5e5afbc76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902847"
---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

デフォルトと呼ばれるオブジェクトを作成します。 列または別名データ型にバインドすると、オブジェクトがバインドされる列 (別名データ型の場合はすべての列) で、挿入時に値が明示的に指定されない場合は、デフォルトによってそれらに挿入される値が指定されます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、ALTER TABLE または CREATE TABLE の DEFAULT キーワードを使用して作成された既定の定義を使用してください。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE DEFAULT [ schema_name . ] default_name   
AS constant_expression [ ; ]  
```  
  
## <a name="arguments"></a>引数  
*schema_name*  
 デフォルトが所属するスキーマの名前を指定します。  
  
*default_name*  
 デフォルトの名前。 デフォルトの名前は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。 既定の所有者名の指定は省略可能です。  
  
*constant_expression*  
定数値のみを含む[式](../../t-sql/language-elements/expressions-transact-sql.md) (列名や他のデータベース オブジェクト名を含めることはできません)。 任意の定数、組み込み関数、または数式を使用できます。別名データ型を含むものは使用できません。 ユーザー定義関数は使用できません。 文字および日付定数は単一引用符 ( **'** ) で囲んでください。金額、整数、および浮動小数点定数には引用符は必要ありません。 バイナリ データの前には 0x を付ける必要があり、通貨データの前にはドル記号 ($) を付ける必要があります。 既定値は、列のデータ型と互換性がある必要があります。  
  
## <a name="remarks"></a>Remarks  
 デフォルト名は現在のデータベース内にのみ作成できます。 データベース内で、既定の名前はスキーマにより一意である必要があります。 デフォルトを作成したら、**sp_bindefault** を使用してデフォルトを列または別名データ型にバインドします。  
  
 デフォルトとバインド先の列に互換性がない場合、既定値の挿入を試みると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってエラー メッセージが生成されます。 たとえば、**numeric** 型の列のデフォルトとして N/A を使用することはできません。  
  
 バインドされている列にとって既定値が長すぎる場合、値は切り捨てられます。  
  
 CREATE DEFAULT ステートメントは、単一のバッチ内で他の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと組み合わせることはできません。  
  
 同じ名前の新しいデフォルトを作成する前に、古いデフォルトを削除する必要があります。 さらに、デフォルトを削除する前に、**sp_unbindefault** を使用してバインドを解除する必要があります。  
  
 列が既定値とそれに関連するルールの両方を持つ場合、既定値はそのルールに従っている必要があります。 ルールに矛盾するデフォルトは挿入できません。挿入を試行すると、そのたびに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではエラー メッセージが表示されます。  
  
 列にバインドすると、次の場合に既定値が挿入されます。  
  
-   値が明示的に挿入されない場合。  
  
-   DEFAULT VALUES または DEFAULT のいずれかのキーワードは、既定値を挿入するために INSERT と共に使用されます。  
  
 列の作成時に NOT NULL が指定され、その列のデフォルトが作成されていない場合、ユーザーがその列に入力を行わないとエラー メッセージが生成されます。 次の表は、デフォルトの有無と、NULL または NOT NULL として定義された列の関係を示しています。 テーブル内のエントリに結果が表示されます。  
  
|列の定義|入力なし、既定値なし|入力なし、デフォルトあり|NULL を入力、デフォルトなし|NULL を入力、既定値あり|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULL|既定値 (default)|NULL|NULL|  
|**NOT NULL**|Error|既定値 (default)|error|error|  
  
 デフォルトの名前を変更するには、**sp_rename** を使用します。 デフォルトに関するレポートを表示するには、**sp_help** を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE DEFAULT を実行するには、ユーザーは少なくとも現在のデータベース内では CREATE DEFAULT 権限を、デフォルトが作成されるスキーマに対しては ALTER 権限を持っている必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-simple-character-default"></a>A. シンプルな文字の既定値を作成する  
 次の例では、"`unknown`" という文字のデフォルトを作成します。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. 既定値をバインドする  
 次の例では、例 A で作成したデフォルトをバインドします。デフォルトが有効になるのは、`Contact` テーブルの `Phone` 列にエントリが指定されていない場合のみです。 
 
 > [!Note] 
 >  任意のエントリを省略することは、INSERT ステートメントで NULL を明示的に示すこととは異なります。  
  
 `phonedflt` という名前のデフォルトは存在しないので、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは失敗します。 これは例示のみを目的としています。  
  
```sql  
USE AdventureWorks2012;  
GO  
sp_bindefault 'phonedflt', 'Person.PersonPhone.PhoneNumber';  
```  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
