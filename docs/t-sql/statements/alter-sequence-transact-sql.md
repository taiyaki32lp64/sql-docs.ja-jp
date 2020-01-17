---
title: ALTER SEQUENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SEQUENCE_TSQL
- ALTER SEQUENCE
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, altering
- ALTER SEQUENCE statement
ms.assetid: decc0760-029e-4baf-96c9-4a64073df1c2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 337b2ee6d7edffeb49c2cee6291d30100b4c1df0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070329"
---
# <a name="alter-sequence-transact-sql"></a>ALTER SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  既存のシーケンス オブジェクトの引数を変更します。 **CACHE** オプションを使用してシーケンスが作成されている場合、シーケンスを変更するとキャッシュが再作成されます。  
  
 シーケンス オブジェクトは、[CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) ステートメントを使用して作成されます。 シーケンスは整数値であり、整数を返す任意のデータ型を指定できます。 このデータ型は、ALTER SEQUENCE ステートメントでは変更できません。 データ型を変更するには、シーケンス オブジェクトを削除して再作成します。  
  
 シーケンスはユーザー定義のスキーマ バインド オブジェクトであり、仕様に従って数値のシーケンスを生成します。 NEXT VALUE FOR 関数を呼び出すことにより、シーケンスから新しい値が生成されます。 一度に複数のシーケンス番号を取得するには、 **sp_sequence_get_range** を使用します。 CREATE SEQUENCE、および **sp_sequence_get_range** と NEXT VALUE FOR 関数の両方を使用する場合の詳細およびシナリオについては、「[シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER SEQUENCE [schema_name. ] sequence_name  
    [ RESTART [ WITH <constant> ] ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE <constant> } | { NO MINVALUE } ]  
    [ { MAXVALUE <constant> } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *sequence_name*  
 データベースに認識されるシーケンスの一意な名前を指定します。 データ型は **sysname** です。  
  
 RESTART [ WITH \<constant> ]  
 シーケンス オブジェクトによって返される次の値です。 RESTART WITH 値を指定する場合は、シーケンス オブジェクトの最小値以上および最大値以下の整数にする必要があります。 WITH 値を省略した場合は、元の CREATE SEQUENCE オプションに基づいてシーケンスの番号付けが再開されます。  
  
 INCREMENT BY \<constant>  
 NEXT VALUE FOR 関数を呼び出すたびに必要なシーケンス オブジェクトの基準値を増分 (負の場合は減少) させるのに使用される値です。 増分値が負の値の場合はシーケンス オブジェクトは降順で、それ以外の場合は昇順です。 0 は増分として使用できません。  
  
 [ MINVALUE \<constant> | NO MINVALUE ]  
 シーケンスのオブジェクトの境界を指定します。 NO MINVALUE を指定すると、シーケンスのデータ型の最小値が使用されます。  
  
 [ MAXVALUE \<constant> | NO MAXVALUE  
 シーケンスのオブジェクトの境界を指定します。 NO MAXVALUE を指定すると、シーケンスのデータ型の最大許容値が使用されます。  
  
 [ CYCLE | NO CYCLE ]  
 このプロパティは、最小値または最大値を超過した場合に、シーケンス オブジェクトを最小値 (降順シーケンス オブジェクトの場合は最大値) から再開するか、例外をスローするかを指定します。  
  
> [!NOTE]  
>  循環後の次の値は最小値または最大値であり、シーケンスの START VALUE ではありません。  
  
 [ CACHE [\<constant> ] | NO CACHE ]  
 生成された値をシステム テーブルに保存するのに必要な IO の数を最小限に抑えることで、シーケンス オブジェクトを使用するアプリケーションのパフォーマンスが向上します。  
  
 キャッシュの動作について詳しくは、「[CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
 シーケンスの作成方法と、シーケンスのキャッシュの管理方法について詳しくは、「[CREATE SEQUENCE &#40;Transact-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)」をご覧ください。  
  
 昇順のシーケンスの MINVALUE と降順のシーケンスの MAXVALUE は、シーケンスの START WITH 値を許可しない値に変更することはできません。 昇順のシーケンスの MINVALUE を START WITH 値より大きい数に変更する、または降順のシーケンスの MAXVALUE を START WITH 値より小さい数に変更するには、RESTART WITH 引数を含めて、最小値と最大値の範囲内にある目的の位置からシーケンスを再開します。  
  
## <a name="metadata"></a>メタデータ  
 シーケンスの詳細については、「 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)」を参照してください。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 シーケンスに対する **ALTER** 権限、またはスキーマに対する **ALTER** 権限が必要です。 シーケンスに対する **ALTER** 権限を許可するには、次の形式で **ALTER ON OBJECT** を使います。  
  
```  
GRANT ALTER ON OBJECT::Test.TinySeq TO [AdventureWorks\Larry]  
```  
  
 シーケンス オブジェクトの所有権は、**ALTER AUTHORIZATION** ステートメントを使って譲渡できます。  
  
### <a name="audit"></a>監査  
 **ALTER SEQUENCE** を監査するには、**SCHEMA_OBJECT_CHANGE_GROUP** を監視します。  
  
## <a name="examples"></a>使用例  
 シーケンスの作成と、**NEXT VALUE FOR** 関数を使用したシーケンス番号の生成の両方の使用例については、「[シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。  
  
### <a name="a-altering-a-sequence"></a>A. シーケンスを変更する  
 次の例では、100 から 200 の範囲の **int** データ型を使って、Test という名前のスキーマと TestSeq という名前のシーケンスを作成します。 シーケンスは 125 で始まり、数値が生成されるたびに 25 ずつ増加します。 シーケンスは循環するように設定されているため、値が最大値の 200 を超えると、最小値の 100 で再開します。  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.TestSeq  
    AS int   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
GO  
```  
  
 次の例では、50 から 200 の範囲を指定して TestSeq シーケンスを変更します。 シーケンスの番号が 100 から再開し、数値が生成されるたびに 50 ずつ増加します。  
  
```  
ALTER SEQUENCE Test. TestSeq  
    RESTART WITH 100  
    INCREMENT BY 50  
    MINVALUE 50  
    MAXVALUE 200  
    NO CYCLE  
    NO CACHE  
;  
GO  
```  
  
 シーケンスが循環しないため、シーケンスが 200 を超えると **NEXT VALUE FOR** 関数はエラーになります。  
  
### <a name="b-restarting-a-sequence"></a>B. シーケンスを再開する  
 次の例では、CountBy1 という名前のシーケンスを作成します。 このシーケンスでは既定値が使用されます。  
  
```  
CREATE SEQUENCE Test.CountBy1 ;  
```  
  
 シーケンスの値を生成するには、所有者は次のステートメントを実行します。  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1  
```  
  
 返される値 -9,223,372,036,854,775,808 は、**bigint** データ型の最小値です。 所有者は、シーケンスを 1 から開始しようとしていたのに、シーケンスの作成時に **START WITH** 句を指定していなかったことに気付きました。 このエラーを修正するには、所有者は次のステートメントを実行します。  
  
```  
ALTER SEQUENCE Test.CountBy1 RESTART WITH 1 ;  
```  
  
 その後、次のステートメントを再度実行して、シーケンス番号を生成します。  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1;  
```  
  
 今度は、想定どおりに番号が 1 になります。  
  
 CountBy1 シーケンスは、9,223,372,036,854,775,807 の数を生成すると操作を中止するようにするために、既定値の NO CYCLE を使用して作成されました。 この後にシーケンス オブジェクトを呼び出すと、エラー 11728 が返されます。 次のステートメントでは、シーケンス オブジェクトが循環するように変更され、キャッシュが 20 に設定されます。  
  
```  
ALTER SEQUENCE Test.CountBy1  
    CYCLE  
    CACHE 20 ;  
  
```  
  
 これにより、シーケンス オブジェクトは 9,223,372,036,854,775,807 に達すると循環し、次の数値はデータ型の最小値である -9,223,372,036,854,775,808 になります。  
  
 所有者は、**bigint** データ型が毎回 8 バイトを使用していることに気付きました。 4 バイトを使用する **int** データ型で十分です。 ただし、シーケンス オブジェクトのデータ型は変更できません。 **int** データ型に変更するには、所有者がこのシーケンス オブジェクトを削除して、適切なデータ型で再作成する必要があります。  
  
## <a name="see-also"></a>参照  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
