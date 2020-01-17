---
title: CREATE SEQUENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SEQUENCE
- CREATE SEQUENCE
- SEQUENCE_TSQL
- CREATE_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SEQUENCE statement
- sequence number object, creating
- sequence object
- number, sequence
ms.assetid: 419f907b-8a72-4d6c-80cb-301df44c24c1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2772440c98d103790808564b5cdddcde4c2dfd42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117179"
---
# <a name="create-sequence-transact-sql"></a>CREATE SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  シーケンス オブジェクトを作成し、そのプロパティを指定します。 シーケンスは、シーケンスが作成された仕様に従って数値のシーケンスを生成するユーザー定義のスキーマ バインド オブジェクトです。 数値のシーケンスは、定義された間隔で昇順または降順に生成され、要求に応じて再起動 (繰り返し) するように構成できます。 ID 列とは異なり、シーケンスは、特定のテーブルに関連付けられていません。 アプリケーションは、シーケンス オブジェクトを参照して、次の値を受け取ります。 シーケンスとテーブルの関係は、アプリケーションによって制御されます。 ユーザー アプリケーションは、シーケンス オブジェクトを参照し、複数の行とテーブル間で値を調整できます。  
  
 行の挿入時に生成される ID 列値とは異なり、アプリケーションは、[NEXT VALUE FOR 関数](../../t-sql/functions/next-value-for-transact-sql.md)を呼び出すことにより、行を挿入せずに次のシーケンス番号を取得できます。 一度に複数のシーケンス番号を取得するには、 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) を使用します。  
  
 **CREATE SEQUENCE** および **NEXT VALUE FOR** 関数を両方使用する場合の詳細およびシナリオについては、「 [シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」をご覧ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE SEQUENCE [schema_name . ] sequence_name  
    [ AS [ built_in_integer_type | user-defined_integer_type ] ]  
    [ START WITH <constant> ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE [ <constant> ] } | { NO MINVALUE } ]  
    [ { MAXVALUE [ <constant> ] } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>引数  
*sequence_name*  
データベースに認識されるシーケンスの一意な名前を指定します。 データ型は **sysname** です。  
  
[ built_in_integer_type | user-defined_integer_type  
シーケンスを任意の整数型として定義できます。 次の型を使用できます。  
  
-   **tinyint** - 0 ～ 255 の範囲  
-   **smallint** - -32,768 ～ 32,767 の範囲  
-   **int** - -2,147,483,648 ～ 2,147,483,647 の範囲  
-   **bigint** - -9,223,372,036,854,775,808 ～ 9,223,372,036,854,775,807 の範囲  
-   小数点以下のない **decimal** と **numeric**。  
-   許可される型のいずれかに基づくユーザー定義データ型 (別名型)。  
  
データ型が指定されていない場合は、**bigint** データ型が既定で使用されます。  
  
START WITH \<constant>  
シーケンス オブジェクトによって返される最初の値。 **START** 値は、シーケンス オブジェクトの最小値以上および最大値以下にする必要があります。 新しいシーケンス オブジェクトの既定の開始値は、昇順のシーケンス オブジェクトの最小値および降順のシーケンス オブジェクトの最大値です。  
  
INCREMENT BY \<constant>  
**NEXT VALUE FOR** 関数を呼び出すたびに必要なシーケンス オブジェクトの値を増分 (負の場合は減少) させるのに使用される値。 増分値が負の値の場合はシーケンス オブジェクトは降順で、それ以外の場合は昇順です。 0 は増分として使用できません。 新しいシーケンス オブジェクトの既定の増分値は 1 です。  
  
[ MINVALUE \<constant> | **NO MINVALUE** ]  
シーケンス オブジェクトの境界を指定します。 新しいシーケンス オブジェクトの既定の最小値は、シーケンス オブジェクトのデータ型の最小値です。 これは、0 を **tinyint** データ型およびその他のすべてのデータ型の負の数。  
  
[ MAXVALUE \<constant> | **NO MAXVALUE**  
シーケンス オブジェクトの境界を指定します。 新しいシーケンス オブジェクトの既定の最大値は、シーケンス オブジェクトのデータ型の最大値です。  
  
[ CYCLE | **NO CYCLE** ]  
最小値または最大値を超過した場合に、シーケンス オブジェクトを最小値 (または降順シーケンス オブジェクトの最大値) から再起動するか、例外をスローするかを指定するプロパティ。 新しいシーケンス オブジェクトの既定のサイクル オプションは、NO CYCLE です。  
  
> [!NOTE]
> SEQUENCE のサイクルは、開始値からではなく最小値または最大値から再起動されることに注意してください。  
  
[ **CACHE** [\<constant> ] | NO CACHE ]  
シーケンス番号を生成するのに必要なディスク IO の数を最小限に抑えることで、シーケンス オブジェクトを使用するアプリケーションのパフォーマンスが向上します。 CACHE の既定値です。  
  
たとえば、キャッシュ サイズとして 50 を選択した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は キャッシュされた 50 の個々の値を保持しません。 現在の値とキャッシュに残っている値の数だけをキャッシュします。 これは、キャッシュを格納するために必要なメモリの量は、常にシーケンス オブジェクトのデータ型の 2 つのインスタンスと等しくなることを意味します。  
  
> [!NOTE]  
> キャッシュ サイズを指定せずにキャッシュ オプションを有効にする場合、データベース エンジンによってサイズが選択されます。 ただし、この選択では一定のサイズが選択されるため、これに依存しないように注意してください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、予告なしにキャッシュ サイズの算出方法を変更する場合があります。  
  
**CACHE** オプションを使用して作成するときに予期しないシャットダウン (電源障害など) が発生すると、キャッシュ内のシーケンス番号が失われる可能性があります。  
  
## <a name="general-remarks"></a>全般的な解説  
 シーケンス番号は、現在のトランザクションの範囲外で生成されます。 シーケンス番号を使用しているトランザクションがコミットまたはロールバックされるかどうかにかかわらず、シーケンス番号は使用されます。 重複の検証は、レコードが完全に設定された後にのみ実行されます。 このため、いくつかのケースでは作成中に同じ番号が複数のレコードに使用されますが、その後重複していると識別されることになります。 このようになったときに他の autonumber 値が後に続くレコードに適用された場合、autonumber 値の間にギャップが生じることがありますが、これは想定されている動作です。
  
### <a name="cache-management"></a>キャッシュ管理  
 パフォーマンスを向上させるため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、引数 **CACHE** によって指定されたシーケンス番号の数を事前に割り当てます。  
  
 たとえば、新しいシーケンスは開始値 1 とキャッシュ サイズ 15 で作成されます。 最初の値が必要な場合は、メモリから 1 から 15 の値を使用します。 最後にキャッシュされた値 (15) は、ディスクのシステム テーブルに書き込まれます。 15 の数値をすべて使用している場合は、次の要求 (16) でキャッシュを再度割り当てます。 最後にキャッシュされた値 (30) は、システム テーブルに書き込まれます。  
  
 22 個の番号を使用した後で[!INCLUDE[ssDE](../../includes/ssde-md.md)]が停止する場合は、メモリ (23) 内にある次のシーケンス番号がシステム テーブルに書き込まれ、以前に格納された数字を上書きします。  
  
 SQL Server が再起動し、シーケンス番号が必要な場合、開始番号はシステム テーブル (23) から読み取られます。 15 の数 (23 から 38) のキャッシュ量がメモリに割り当てられ、次の非キャッシュ番号 (39) がシステム テーブルに書き込まれます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]が電源障害などのイベントで異常停止した場合、シーケンスはシステム テーブル (39) から読み取られた数で再起動されます。 メモリに割り当てられたシーケンス番号 (ただし、ユーザーやアプリケーションから要求されていないもの) は失われます。 この機能によってギャップが残る場合がありますが、単一のシーケンス オブジェクトが **CYCLE** として定義されていないか、または手動で再起動されない限り、同じ値が単一のシーケンス オブジェクトに対して 2 回発行されることはありません。  
  
 キャッシュは、現在の値 (発行された最後の値) とキャッシュに残っている値の数を追跡することによって、メモリに維持されます。 したがって、キャッシュによって使用されるメモリの量は、常にシーケンス オブジェクトのデータ型の 2 つのインスタンスと等しくなります。  
  
 キャッシュの引数を **NO CACHE** に設定すると、シーケンスが使用されるたびに現在のシーケンス値がシステム テーブルに書き込まれます。 これにより、ディスク アクセスが増えてパフォーマンスが低下する場合がありますが、意図しないギャップが発生する可能性は低減されます。 **NEXT VALUE FOR** または **sp_sequence_get_range** 関数を使用して数値を要求する場合でもギャップが発生することはありますが、数値は、コミットされていないトランザクションで使用される場合も、使用されない場合もあります。  
  
 シーケンス オブジェクトで **CACHE** オプションを使用するとき、シーケンス オブジェクトを再起動する場合、または **INCREMENT**、**CYCLE**、**MINVALUE**、**MAXVALUE** やキャッシュ サイズ プロパティを変更する場合は、変更が発生する前にキャッシュがシステム テーブルに書き込まれます。 キャッシュは、現在の値から開始して再書き込みされます (つまり、スキップされる番号はありません)。 キャッシュ サイズを変更すると、即座に反映されます。  
  
 **キャッシュされた値が使用可能なときの CACHE オプション**  
  
 シーケンス オブジェクトのメモリ内キャッシュで利用できる未使用の値が存在する場合は、**CACHE** オプションの次の値を生成するようにシーケンス オブジェクトが要求されるたびに、以下のプロセスが発生します。  
  
1.  シーケンス オブジェクトの次の値が計算される。  
  
2.  シーケンス オブジェクトの新しい現在の値は、メモリ内で更新される。  
  
3.  計算された値は、呼び出し元のステートメントに返される。  
  
**キャッシュが空になった場合の CACHE オプション**  
  
 キャッシュが空になった場合は、**CACHE** オプションの次の値を生成するようにシーケンス オブジェクトが要求されるたびに、以下のプロセスが発生します。  
  
1.  シーケンス オブジェクトの次の値が計算される。  
  
2.  新しいキャッシュの最後の値が計算される。  
  
3.  シーケンス オブジェクトのシステム テーブル行がロックされ、手順 2. (最後の値) で計算された値がシステム テーブルに書き込まれる。 キャッシュが空になったイベントが発生し、新しい永続化された値がユーザーに通知されます。  
  
**NO CACHE オプション**  
  
 **NO CACHE** オプションの次の値を生成するようにシーケンス オブジェクトが要求されるたびに、以下のプロセスが発生します。  
  
1.  シーケンス オブジェクトの次の値が計算される。  
  
2.  シーケンス オブジェクトの新しい現在の値は、システム テーブルに書き込まれる。  
  
3.  計算された値は、呼び出し元のステートメントに返される。  
  
## <a name="metadata"></a>メタデータ  
 シーケンスの詳細については、「 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)」を参照してください。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 SCHEMA に対する **CREATE SEQUENCE**権限、 **ALTER**権限、または **CONTROL** 権限が必要です。  
  
-   db_owner および db_ddladmin 固定データベース ロールのメンバーは、シーケンス オブジェクトを作成、変更、および削除できます。  
  
-   db_owner および db_datawriter 固定データベース ロールのメンバーは、シーケンス オブジェクトで番号を生成することによって、シーケンス オブジェクトを更新できます。  
  
 次の例では、ユーザーの AdventureWorks\Larry テストのスキーマでシーケンスを作成するためのアクセス許可を付与します。  
  
```sql  
GRANT CREATE SEQUENCE ON SCHEMA::Test TO [AdventureWorks\Larry]  
```  
  
 シーケンス オブジェクトの所有権は、**ALTER AUTHORIZATION** ステートメントを使って譲渡できます。  
  
 シーケンスがユーザー定義のデータ型を使用している場合、シーケンスの作成者にはその型の REFERENCES 権限が必要です。  
  
### <a name="audit"></a>監査  
 **CREATE SEQUENCE** を監査するには、**SCHEMA_OBJECT_CHANGE_GROUP** を監視します。  
  
## <a name="examples"></a>使用例  
 シーケンスを作成し、**NEXT VALUE FOR** 関数を使用してシーケンス番号を生成する例については、「[シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。  
  
 ほとんどの次の例では、テストをという名前のスキーマでシーケンス オブジェクトを作成します。  
  
 テストのスキーマを作成するには、次のステートメントを実行します。  
  
```sql  
CREATE SCHEMA Test ;  
GO  
```  
  
### <a name="a-creating-a-sequence-that-increases-by-1"></a>A. 1 つずつ増加するシーケンスを作成する  
 次の例では、Thierry は、it が使用されるたびに増加する CountBy1 をいずれかによってという名前のシーケンスを作成します。  
  
```sql  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="b-creating-a-sequence-that-decreases-by-1"></a>B. 1 つずつ減少するシーケンスを作成する  
 次の例では、シーケンスは 0 から開始し、使用するたびに 1 つずつ減少します。  
  
```sql  
CREATE SEQUENCE Test.CountByNeg1  
    START WITH 0  
    INCREMENT BY -1 ;  
GO  
```  
  
### <a name="c-creating-a-sequence-that-increases-by-5"></a>C. 5 つずつ増加するシーケンスを作成する  
 次の例では、使用されるたびに 5 つずつ増加するシーケンスを作成します。  
  
```sql  
CREATE SEQUENCE Test.CountBy1  
    START WITH 5  
    INCREMENT BY 5 ;  
GO  
```  
  
### <a name="d-creating-a-sequence-that-starts-with-a-designated-number"></a>D. 指定された数値から開始するシーケンスを作成する  
 テーブルをインポートした後、Thierry は最上位の ID 番号が 24,328 であることに気付きます。 Thierry には、24,329 で始まる番号を生成するシーケンスが必要です。 次のコードは 24,329 で始まり、1 ずつ増加するシーケンスを作成します。  
  
```sql  
CREATE SEQUENCE Test.ID_Seq  
    START WITH 24329  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="e-creating-a-sequence-using-default-values"></a>E. 既定値を使用してシーケンスを作成する  
 次の例では、既定値を使用して、シーケンスを作成します。  
  
```sql  
CREATE SEQUENCE Test.TestSequence ;  
```  
  
 次のステートメントを実行して、シーケンスのプロパティを確認します。  
  
```sql  
SELECT * FROM sys.sequences WHERE name = 'TestSequence' ;  
```  
  
 出力の一覧の一部は、既定値を示します。  
  
|||  
|-|-|  
|`start_value`|`-9223372036854775808`|  
|`increment`|`1`|  
|`mimimum_value`|`-9223372036854775808`|  
|`maximum_value`|`9223372036854775807`|  
|`is_cycling`|`0`|  
|`is_cached`|`1`|  
|`current_value`|`-9223372036854775808`|  
  
### <a name="f-creating-a-sequence-with-a-specific-data-type"></a>F. 特定のデータ型のシーケンスを作成する  
 次の例では、-32,768 ～ 32,767 の範囲の **smallint** データ型を使用して、シーケンスを作成します。  
  
```sql  
CREATE SEQUENCE SmallSeq 
    AS smallint ;  
```  
  
### <a name="g-creating-a-sequence-using-all-arguments"></a>G. すべての引数を使用してシーケンスを作成する  
 次の例では、0 ～ 255 の範囲の **smallint** データ型を使用して、DecSeq という名前のシーケンスを作成します。 シーケンスは 125 で始まり、数値が生成されるたびに 25 ずつ増加します。 シーケンスは、値が最大値の 200 を超える場合は繰り返すように設定されているため、最小値の 100 で再起動します。  
  
```sql  
CREATE SEQUENCE Test.DecSeq  
    AS decimal(3,0)   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
```  
  
 次のステートメントを実行して、最初の値、つまり `START WITH` オプションが 125であることを確認します。  
  
```sql  
SELECT NEXT VALUE FOR Test.DecSeq;  
```  
  
 150、175、200 を返すように、ステートメントを 3 回実行します。  
  
 ステートメントを再度実行し、開始値が `MINVALUE` オプション (100) に戻ることを確認します。  
  
 次のコードを実行して、キャッシュ サイズを確認し、現在の値を表示します。  
  
```sql  
SELECT cache_size, current_value   
FROM sys.sequences  
WHERE name = 'DecSeq' ;  
```  
  
## <a name="see-also"></a>参照  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
