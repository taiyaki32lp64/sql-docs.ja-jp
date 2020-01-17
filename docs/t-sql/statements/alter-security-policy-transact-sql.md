---
title: ALTER SECURITY POLICY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SECURITY_POLICY_TSQL
- ALTER SECURITY POLICY
- ALTER_SECURITY_TSQL
- ALTER SECURITY
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER SECURITY POLICY statement
ms.assetid: a8efc37e-113d-489c-babc-b914fea2c316
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 458083fda6382c353af78c7d2b438fdc0d39c826
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2019
ms.locfileid: "72173855"
---
# <a name="alter-security-policy-transact-sql"></a>ALTER SECURITY POLICY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

セキュリティ ポリシーを変更します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
ALTER SECURITY POLICY schema_name.security_policy_name   
    (  
        { ADD { FILTER | BLOCK } PREDICATE tvf_schema_name.security_predicate_function_name   
           ( { column_name | arguments } [ , ...n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ]  }   
        | { ALTER { FILTER | BLOCK } PREDICATE tvf_schema_name.new_security_predicate_function_name   
             ( { column_name | arguments } [ , ...n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ] }  
        | { DROP { FILTER | BLOCK } PREDICATE ON table_schema_name.table_name }   
        | [ <additional_add_alter_drop_predicate_statements> [ , ...n ] ]  
    )    [ WITH ( STATE = { ON | OFF } ) ]  
    [ NOT FOR REPLICATION ]  
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>引数  
security_policy_name  
セキュリティ ポリシーの名前。 セキュリティ ポリシー名は識別子のルールに準拠し、データベースおよびそのスキーマで一意である必要があります。  
  
schema_name  
セキュリティ ポリシーが属するスキーマの名前。 *schema_name* はスキーマのバインドのために必要です。  
  
[ FILTER | BLOCK ]  
ターゲット テーブルにバインドされている関数のセキュリティの述語の型。 FILTER 述語は、読み取り操作が可能な行を通知なしにフィルター処理します。 BLOCK 述語は、その述語関数に違反する書き込み操作を明示的に禁止します。  
  
tvf_schema_name.security_predicate_function_name  
述語として使用され、ターゲット テーブルに対するクエリで実施されるインライン テーブル値関数。 特定のテーブルの特定の DML 操作に対して定義できるセキュリティ述語の数は 1 つです。 SCHEMABINDING オプションを使用してインライン テーブル値関数を作成します。  
  
{ column_name | arguments }  
セキュリティ述語関数のパラメーターとして使用される列名または式。 ターゲット テーブル上の任意の列を、述語関数の引数として使用できます。 リテラルを含む式、ビルトイン、および算術演算子を使用する式を利用できます。  
  
*table_schema_name.table_name*  
セキュリティ述語のターゲット テーブル。 セキュリティが無効になっている複数のポリシーでは、特定の DML 操作に対して、1 つのテーブルを対象にできますが、有効にできるのはどの時点でも 1 つだけです。  
  
*\<block_dml_operation>*  
適用されたブロック述語の特定の DML 操作。 AFTER は、DML 操作 (INSERT または UPDATE) が実行された後に、行の値に対して述語が評価されることを指定します。 BEFORE は、DML 操作 (INSERT または UPDATE) が実行される前に、行の値に対して述語が評価されることを指定します。 操作が指定されていない場合、述語は、すべての操作に適用されます。  
  
適用されたブロック述語の操作は、述語を一意に特定するために使用されるため、その操作を ALTER することはできません。 代わりに、その述語を削除して、新しい 2 つの操作用に新しい述語を追加する必要があります。  
  
WITH ( STATE = { ON | OFF } )  
セキュリティ ポリシーによるターゲット テーブルに対するセキュリティ述語の実施を有効または無効にします。 指定しないと、作成されているセキュリティ ポリシーは有効になります。  
  
NOT FOR REPLICATION  
レプリケーション エージェントがターゲット オブジェクトを変更するときに、セキュリティ ポリシーを実行してはならないことを示します。 詳細については、「[同期中にトリガと制約の動作を制御する方法 &#40;レプリケーション Transact-SQL プログラミング&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)」を参照してください。  
  
table_schema_name.table_name  
適用されたセキュリティ述語のターゲット テーブル。 無効な複数のセキュリティ ポリシーは単一テーブルをターゲットにできますが、有効にできるのはどの時点でも 1 つだけです。  
  
## <a name="remarks"></a>Remarks  
ALTER SECURITY POLICY ステートメントはトランザクションのスコープ内にあります。 トランザクションがロールバックされると、ステートメントもロールバックされます。  
  
メモリ最適化テーブルで述語関数を使用する場合、セキュリティ ポリシーには **SCHEMABINDING** が含まれる必要があり、**WITH NATIVE_COMPILATION** コンパイル ヒントを使用する必要があります。 SCHEMABINDING の引数は、すべての述語に適用されるため、ALTER ステートメントを使用して変更できません。 スキーマ バインドを変更するには、セキュリティ ポリシーを削除して再作成する必要があります。  
  
ブロック述語は、対応する DML 操作を実行した後に評価されます。 そのため、READ UNCOMMITTED のクエリでは、ロールバックされる一時的な値を確認できます。  
  
## <a name="permissions"></a>アクセス許可  
ALTER ANY SECURITY POLICY 権限が必要です。  
  
また、追加される各述語に関しては次のアクセス許可も必要になります。  
  
-   述語として使用している関数に関する SELECT および REFERENCES 権限。  
-   ポリシーにバインドしているターゲット テーブルに対する REFERENCES 権限。  
-   引数として使用しているターゲット テーブルのすべての列に対する REFERENCES 権限。  
  
## <a name="examples"></a>使用例  
以下の例は、**ALTER SECURITY POLICY** 構文の使用法を示しています。 詳細なセキュリティ ポリシーのシナリオ例については、「[行レベルのセキュリティ](../../relational-databases/security/row-level-security.md)」をご覧ください。  
  
### <a name="a-adding-an-additional-predicate-to-a-policy"></a>A. ポリシーに述語を追加する  
以下の構文はセキュリティ ポリシーを変更します。その際、`mytable` テーブルにフィルター述語を追加します。  
  
```  
ALTER SECURITY POLICY pol1   
    ADD FILTER PREDICATE schema_preds.SecPredicate(column1)   
    ON myschema.mytable;  
```  
  
### <a name="b-enabling-an-existing-policy"></a>B. 既存のポリシーを有効にする  
以下の例では、ALTER 構文を使用してセキュリティ ポリシーを有効にします。  
  
```  
ALTER SECURITY POLICY pol1 WITH ( STATE = ON );  
```  
  
### <a name="c-adding-and-dropping-multiple-predicates"></a>C. 複数の述語を追加または削除する  
以下の構文ではセキュリティ ポリシーを変更します。その際、`mytable1` テーブルと `mytable3` テーブルにフィルター述語を追加し、`mytable2` テーブルからフィルター述語を削除します。  
  
```  
ALTER SECURITY POLICY pol1  
ADD FILTER PREDICATE schema_preds.SecPredicate1(column1)   
    ON myschema.mytable1,  
DROP FILTER PREDICATE   
    ON myschema.mytable2,  
ADD FILTER PREDICATE schema_preds.SecPredicate2(column2, 1)   
    ON myschema.mytable3;  
```  
  
### <a name="d-changing-the-predicate-on-a-table"></a>D. テーブルの述語を変更する  
以下の構文は、mytable テーブルの既存のフィルター述語を SecPredicate2 関数になるように変更します。  
  
```  
ALTER SECURITY POLICY pol1  
    ALTER FILTER PREDICATE schema_preds.SecPredicate2(column1)  
        ON myschema.mytable;  
```  
  
### <a name="e-changing-a-block-predicate"></a>E. ブロック述語を変更する  
テーブルの操作に対するブロック述語関数を変更します。  
  
```  
ALTER SECURITY POLICY rls.SecPol  
    ALTER BLOCK PREDICATE rls.tenantAccessPredicate_v2(TenantId) 
    ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>参照  
[行レベルのセキュリティ](../../relational-databases/security/row-level-security.md)   
[CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
[DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
[sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
[sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  
