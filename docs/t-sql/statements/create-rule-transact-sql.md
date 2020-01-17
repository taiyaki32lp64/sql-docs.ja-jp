---
title: CREATE RULE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RULE_TSQL
- CREATE RULE
- CREATE_RULE_TSQL
- RULE
dev_langs:
- TSQL
helpviewer_keywords:
- list rules [SQL Server]
- unbinding rules
- pattern rules [SQL Server]
- range rules [SQL Server]
- alias data types [SQL Server], rules
- CREATE RULE statement
- reports [SQL Server], rules
- status information [SQL Server], rules
- rules [SQL Server], precedence
- binding rules [SQL Server]
- rules [SQL Server], creating
ms.assetid: b016a289-3a74-46b1-befc-a13183be51e4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0e0a46138b9e6c4ccaff09c1ab5261f739deb6b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006495"
---
# <a name="create-rule-transact-sql"></a>CREATE RULE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ルールと呼ばれるオブジェクトを作成します。 ルールを列または別名データ型にバインドすると、その列に挿入できる適切な値を制限できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]代わりに CHECK 制約を使用することをお勧めします。 CHECK 制約は、CREATE TABLE または ALTER TABLE の CHECK キーワードを使用して作成されます。 詳細については、「 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)」を参照してください。  
  
 1 つの列または別名データ型にバインドできるルールは 1 つだけです。 ただし、1 つの列には 1 つのルールと複数の CHECK 制約を関連付けることができます。 これが True の場合、すべての制限が評価されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE RULE [ schema_name . ] rule_name   
AS condition_expression  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *schema_name*  
 ルールが属しているスキーマの名前を指定します。  
  
 *rule_name*  
 新しいルールの名前です。 ルール名は、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 ルールの所有者名の指定は省略可能です。  
  
 *condition_expression*  
 ルールを定義する条件を指定します。 ルールには、WHERE 句で有効な任意の式を指定できます。また、算術演算子、関係演算子、述語 (IN、LIKE、BETWEEN など) のような要素も含めることができます。 ルールでは、列や別のデータベース オブジェクトを参照することはできません。 データベース オブジェクトを参照しない組み込み関数は含めることができます。 またユーザー定義関数は使用できません。  
  
 *condition_expression* には 1 つの変数が含まれます。 それぞれのローカル変数の前には、アット マーク ( **@** ) を付けます。 この式では、UPDATE または INSERT ステートメントで入力された値を参照します。 ルールを作成するときには、任意の名前または記号で値を表すことができますが、最初の文字はアット マーク ( **@** ) にする必要があります。  
  
> [!NOTE]  
>  別名データ型を使用する式にルールを作成することは避けてください。 別名データ型を使用する式にルールを作成することはできますが、ルールを列または別名データ型にバインドすると、参照時にこの式のコンパイルに失敗します。  
  
## <a name="remarks"></a>Remarks  
 CREATE RULE は、単一のバッチ内で他の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと組み合わせて使用することはできません。 ルールを作成した時点では、データベース内の既存のデータにルールは適用されません。また、ルールをシステム データ型にバインドすることはできません。  
  
 ルールは、現在のデータベース内でのみ作成できます。 ルールを作成したら、**sp_bindrule** を実行してルールを列または別名データ型にバインドします。 ルールと列のデータ型の間には互換性がとれている必要があります。 たとえば、数値型列のルールとして "\@value LIKE A%" は使用できません。 **text**、**ntext**、**image**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**xml**、CLR ユーザー定義型、**timestamp** の列には、ルールをバインドできません。 ルールは計算列にバインドできません。  
  
 文字および日付定数は、必ず単一引用符 (') で囲み、バイナリ定数は 0x で始めてください。 ルールとバインド先の列の間に互換性がとれていない場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]では、ルールがバインドされたときではなく値が挿入されたときにエラー メッセージが返されます。  
  
 別名データ型にバインドされたルールは、別名データ型のデータベース列に値を挿入するとき、または列を更新するときにのみアクティブになります。 ルールでは変数はテストされないため、別名データ型変数には、同じデータ型の列にバインドしたルールによって拒否されるような値を割り当てないでください。  
  
 ルールに関するレポートを取得するには、**sp_help** を使用します。 ルールのテキストを表示するには、ルール名をパラメーターに使用して **sp_helptext** を実行します。 ルール名を変更するには、**sp_rename** を使用します。  
  
 同じ名前の新しいルールを作成するときには、まず **sp_unbindrule** を実行して現在のルールのバインドを解除し、次に DROP RULE を使用してルールを削除する必要があります。 列からルールのバインドを解除するには、**sp_unbindrule** を使用します。  
  
 以前のルールのバインドを解除せずに、新しいルールを列またはデータ型にバインドすることができます。新しいルールは以前のルールをオーバーライドします。 列にバインドされているルールは、別名データ型にバインドされているルールよりも常に優先されます。 ルールを列にバインドすると、その列の別名データ型に既にバインドされていたルールは新しいルールに置き換えられます。 ルールをデータ型にバインドしても、その別名データ型の列にバインドされていたルールは新しいルールに置き換えられません。 次の表は、ルールが既に存在する列および別名データ型にルールをバインドするときの優先順位です。  
  
|新しいルールのバインド先|前のルールのバインド先が<br /><br /> 別名データ型の場合|前のルールのバインド先が<br /><br /> [列]|  
|-----------------------|-------------------------------------------|----------------------------------|  
|別名データ型|前のルールが置き換えられる|変更なし|  
|[列]|前のルールが置き換えられる|前のルールが置き換えられる|  
  
 列に既定値とルールの両方が関連付けられている場合、既定値はルールによって定義されるドメイン内のものであることが必要です。 ルールに矛盾する既定値は挿入されません。 SQL Server データベース エンジンでは、既定値の挿入が試行されるたびにエラー メッセージが生成されます。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE RULE を実行するために、ユーザーには少なくとも、現在のデータベースの CREATE RULE 権限と、ルールを作成するスキーマの ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-rule-with-a-range"></a>A. 範囲を指定してルールを作成する  
 次の例で作成するルールは、ルールのバインド先となる列に挿入できる整数の範囲を制限します。  
  
```  
CREATE RULE range_rule  
AS   
@range>= $1000 AND @range <$20000;  
```  
  
### <a name="b-creating-a-rule-with-a-list"></a>B. リストを指定してルールを作成する  
 次の例で作成するルールは、ルールのバインド先となる列に挿入できる値を、指定したリストの値に制限します。  
  
```  
CREATE RULE list_rule  
AS   
@list IN ('1389', '0736', '0877');  
```  
  
### <a name="c-creating-a-rule-with-a-pattern"></a>C. パターンを指定してルールを作成する  
 次の例では、任意の文字 2 つの後にハイフン (`-`)、その後に任意の数の文字 (または文字なし)、最後に `0` ～ `9` の整数 1 文字というパターンを指定するルールを作成します。  
  
```  
CREATE RULE pattern_rule   
AS  
@value LIKE '__-%[0-9]'  
```  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
