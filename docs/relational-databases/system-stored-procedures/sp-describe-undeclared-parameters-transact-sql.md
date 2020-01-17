---
title: sp_describe_undeclared_parameters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_undeclared_parameters
- sp_describe_undeclared_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_undeclared_parameters
ms.assetid: 6f016da6-dfee-4228-8b0d-7cd8e7d5a354
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1205572235b141709cd463476182d9b405446188
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908325"
---
# <a name="sp_describe_undeclared_parameters-transact-sql"></a>sp_describe_undeclared_parameters (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ内の宣言されていないパラメーターに関するメタデータを含む結果セットを返します。 **\@tsql**バッチで使用されているが **\@params**で宣言されていない各パラメーターを考慮します。 結果セットが返されます。この結果セットには、そのパラメーターに対して推測される型情報が含まれる、このようなパラメーターごとに1行のデータが含まれます。 **\@tsql**入力バッチに、 **\@params**で宣言されているパラメーター以外のパラメーターがない場合、このプロシージャは空の結果セットを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql
  
sp_describe_undeclared_parameters   
    [ @tsql = ] 'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' data type ] [, ...n]  
```  
  
## <a name="arguments"></a>引数  
1つ以上の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを `[ \@tsql = ] 'Transact-SQL\_batch'` します。 *Transact-sql SQL_batch*は**nvarchar (** _n_ **)** または**nvarchar (max)** です。  
  
`[ \@params = ] N'parameters'` \@params は sp_executesql の動作と同様に、[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチのパラメーターの宣言文字列を提供します。 *パラメーター*には、 **nvarchar (** _n_ **)** または**nvarchar (max)** を指定できます。  
  
 は、 *Transact SQL_batch*に埋め込まれているすべてのパラメーターの定義を含む1つの文字列です。 この文字列は Unicode 定数または Unicode 変数にする必要があります。 各パラメーター定義は、パラメーター名とデータ型で構成されます。 n は、追加のパラメーター定義を示すプレースホルダーです。 ステートメント内の Transact-sql ステートメントまたはバッチにパラメーターが含まれていない場合、\@params は必要ありません。 このパラメーターの既定値は NULL です。  
  
 Datatype  
 パラメーターのデータ型です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合、 **sp_describe_undeclared_parameters**は常に戻り値0を返します。 プロシージャがエラーをスローし、プロシージャが RPC として呼び出された場合、返される状態は、dm_exec_describe_first_result_set の error_type 列で説明されているエラーの種類によって設定されます。 プロシージャが [!INCLUDE[tsql](../../includes/tsql-md.md)]から呼び出された場合、エラーが発生した場合でも、戻り値は常に0になります。  
  
## <a name="result-sets"></a>結果セット  
 **sp_describe_undeclared_parameters**は、次の結果セットを返します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int NOT NULL**|結果セット内のパラメーターの位置を表す序数を格納します。 最初のパラメーターの位置は 1 で指定されます。|  
|**name**|**sysname NOT NULL**|パラメーターの名前を格納します。|  
|**suggested_system_type_id**|**int NOT NULL**|に指定されているパラメーターのデータ型の**system_type_id**を格納します。<br /><br /> CLR 型の場合、 **system_type_name**列が NULL を返す場合でも、この列は値240を返します。|  
|**suggested_system_type_name**|**nvarchar (256) NULL**|データ型の名前を格納します。 パラメーターのデータ型に対して指定された引数 (長さ、有効桁数、小数点以下桁数など) を含めます。 データ型がユーザー定義の別名型の場合は、基になるシステム型がここで指定されます。 CLR ユーザー定義データ型である場合は、この列に NULL が返されます。 パラメーターの型を推測できない場合は、NULL が返されます。|  
|**suggested_max_length**|**smallint NOT NULL**|「Sys. 列」を参照してください。 **max_length**列の説明。|  
|**suggested_precision**|**tinyint NOT NULL**|「Sys. 列」を参照してください。 有効桁数列の説明。|  
|**suggested_scale**|**tinyint NOT NULL**|「Sys. 列」を参照してください。 スケール列の説明。|  
|**suggested_user_type_id**|**int NULL**|CLR 型と別名型の場合、sys.types で指定された列のデータ型の user_type_id を格納します。 それ以外の場合は NULL です。|  
|**suggested_user_type_database**|**sysname NULL**|CLR 型と別名型の場合、その型が定義されたデータベースの名前を格納します。 それ以外の場合は NULL です。|  
|**suggested_user_type_schema**|**sysname NULL**|CLR 型と別名型の場合、その型が定義されたスキーマの名前を格納します。 それ以外の場合は NULL です。|  
|**suggested_user_type_name**|**sysname NULL**|CLR 型と別名型の場合、その型の名前を格納します。 それ以外の場合は NULL です。|  
|**suggested_assembly_qualified_type_name**|**nvarchar (4000) NULL**|CLR 型の場合は、型を定義するアセンブリおよびクラスの名前を返します。 それ以外の場合は NULL です。|  
|**suggested_xml_collection_id**|**int NULL**|パラメーターのデータ型の xml_collection_id を格納します。これは、sys. columns で指定されています。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**suggested_xml_collection_database**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションが定義されているデータベースを格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**suggested_xml_collection_schema**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションが定義されているスキーマを格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**suggested_xml_collection_name**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションの名前を格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**suggested_is_xml_document**|**bit NOT NULL**|返される型が XML であり、その型が XML ドキュメントであることが保証されている場合は1を返します。 それ以外の場合は0を返します。|  
|**suggested_is_case_sensitive**|**bit NOT NULL**|列が大文字と小文字を区別する文字列型の場合は1、それ以外の場合は0を返します。|  
|**suggested_is_fixed_length_clr_type**|**bit NOT NULL**|この列が固定長の CLR 型の場合は 1、それ以外の場合は 0 を返します。|  
|**suggested_is_input**|**bit NOT NULL**|パラメーターが代入の左辺以外の場所で使用されている場合は1を返します。 それ以外の場合は0を返します。|  
|**suggested_is_output**|**bit NOT NULL**|パラメーターが代入の左辺で使用されているか、ストアドプロシージャの出力パラメーターに渡された場合、1を返します。 それ以外の場合は0を返します。|  
|**formal_parameter_name**|**sysname NULL**|パラメーターがストアド プロシージャまたはユーザー定義関数の引数の場合は、対応する仮パラメーターの名前を返します。 それ以外の場合は NULL を返します。|  
|**suggested_tds_type_id**|**int NOT NULL**|内部使用です。|  
|**suggested_tds_length**|**int NOT NULL**|内部使用です。|  
  
## <a name="remarks"></a>Remarks  
 **sp_describe_undeclared_parameters**は常に0の戻り値の状態を返します。  
  
 最も一般的な使用方法は、パラメーターを含み、それらのパラメーターを任意の方法で処理する必要がある [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがアプリケーションで指定される場合です。 例としては、ユーザーが ODBC パラメーター構文を使用してクエリを提供するユーザーインターフェイス (ODBCTest や RowsetViewer など) があります。 アプリケーションは、パラメーターの数を動的に検出し、各パラメーターの入力をユーザーに求める必要があります。  
  
 別の例として、ユーザー入力なしで、アプリケーションがパラメーターをループして、そのデータを他の場所 (テーブルなど) から取得する必要がある場合が挙げられます。 この場合は、アプリケーションはすべてのパラメーター情報を一度に渡す必要はありません。 代わりに、アプリケーションはプロバイダーからすべてのパラメーター情報を取得し、テーブルからデータ自体を取得することができます。 **Sp_describe_undeclared_parameters**を使用するコードはより汎用的で、データ構造が後で変更される場合に変更が必要になる可能性は低くなります。  
  
 **sp_describe_undeclared_parameters**は、次のいずれかの場合にエラーを返します。  
  
-   入力 \@tsql が有効な [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチではない場合。 有効性は、[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチの解析と分析によって決定されます。 クエリの最適化中または実行中のバッチによって発生したエラーは、[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチが有効かどうかを判断する際には考慮されません。  
  
-   \@params が NULL ではなく、パラメーターに対して構文的に有効な宣言文字列ではない文字列が含まれている場合、またはパラメーターに複数回を宣言する文字列が含まれている場合。  
  
-   入力 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチが \@params で宣言されたパラメーターと同じ名前のローカル変数を宣言している場合。  
  
- ステートメントが一時テーブルを参照している場合。

- クエリには、パーマネントテーブルの作成が含まれ、その後クエリが実行されます。
  
 \@params で宣言されたパラメーター以外のパラメーターが \@tsql にない場合、このプロシージャは空の結果セットを返します。  
  
## <a name="parameter-selection-algorithm"></a>パラメーター選択アルゴリズム  
 宣言されていないパラメーターを持つクエリの場合、宣言されていないパラメーターのデータ型の推論は、3つの手順で行われます。  
  
 **手順1**  
  
 宣言されていないパラメーターを持つクエリのデータ型の推論の最初の手順は、宣言されていないパラメーターに依存しないデータ型を持つすべてのサブ式のデータ型を見つけることです。 型は、次の式に対して決定できます。  
  
-   列、定数、変数、および宣言されたパラメーター。  
  
-   ユーザー定義関数 (UDF) の呼び出しの結果。  
  
-   すべての入力に対して宣言されていないパラメーターに依存しないデータ型を持つ式。  
  
 たとえば、クエリ `SELECT dbo.tbl(@p1) + c1 FROM t1 WHERE c2 = @p2 + 2`を考えてみます。 式 dbo... (\@p1) + c1 および c2 にはデータ型があり、expression \@p1 と \@p2 + 2 には含まれません。  
  
 この手順の実行後、UDF の呼び出し以外の任意の式に、データ型のない 2 つの引数が含まれている場合、型推論はエラーで失敗します。 たとえば、次のすべての式ではエラーが発生します。  
  
```sql
SELECT * FROM t1 WHERE @p1 = @p2  
SELECT * FROM t1 WHERE c1 = @p1 + @p2  
SELECT * FROM t1 WHERE @p1 = SUBSTRING(@p2, 2, 3)  
```  
  
 次の例では、エラーは生成されません。  
  
```sql
SELECT * FROM t1 WHERE @p1 = dbo.tbl(c1, @p2, @p3)  
```
  
 **手順2**  
  
 宣言されていないパラメーター \@p の場合、型推論アルゴリズムは \@p を含む最も内側の式 E (\@p) を検索し、次のいずれかになります。  
  
-   比較演算子または代入演算子の引数。  
  
-   ユーザー定義関数 (テーブル値 UDF を含む)、プロシージャ、またはメソッドの引数。  
  
-   **INSERT**ステートメントの**VALUES**句の引数。  
  
-   **キャスト**または**変換**の引数。  
  
 型推論アルゴリズムでは、E (\@p) の対象データ型 TT (\@p) が検索されます。 前の例のターゲットデータ型は次のとおりです。  
  
-   比較または代入の反対側のデータ型。  
  
-   この引数が渡されるパラメーターの宣言されたデータ型。  
  
-   この値が挿入される列のデータ型。  
  
-   ステートメントがキャストまたは変換されるデータ型。  
  
 たとえば、クエリ `SELECT * FROM t WHERE @p1 = dbo.tbl(@p2 + c1)`を考えてみます。 次に、E (\@p1) = \@p1、E (\@p2) = \@p2 + c1、TT (\@p1) は、宣言された戻り値のデータ型は dbo です。 TT (\@p2) は、dbo. データ型の宣言されたパラメーターのデータ型です。  
  
 \@p が手順2の先頭に記載されている式に含まれていない場合、型推論アルゴリズムは、E (\@p) が \@p を含む最大のスカラー式であると判断し、型推論アルゴリズムは E (\@p) のターゲットデータ型 TT (\@p) を計算しません。 たとえば、クエリが SELECT `@p + 2` の場合、E (\@p) = \@p + 2,、TT (\@p) はありません。  
  
 **手順 3.**  
  
 E (\@p) と TT (\@p) が識別されたので、型推論アルゴリズムは、次の2つの方法のいずれかで、\@p のデータ型を推測します。  
  
-   単純な推論  
  
     E (\@p) = \@p と TT (\@p) が存在する場合、\@つまり、p が手順 2. の先頭に記載されているいずれかの式に直接引数として指定されていると、型推論アルゴリズムによって \@p のデータ型が TT (\@p) に推測されます。 例 :  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p1 AND @p2 = dbo.tbl(@p3)  
    ```  
  
     \@p1、\@p2、および \@p3 のデータ型は、c1 のデータ型、戻り値のデータ型は、それぞれ、dbo. データ型になります。  
  
     特殊なケースとして \@p が \<、>、\<=、または > = 演算子の引数である場合、単純な推論の規則は適用されません。 型推論アルゴリズムでは、次のセクションで説明する一般的な推論ルールが使用されます。 たとえば、c1 がデータ型 char(30) の列である場合に、以下の 2 つのクエリについて考えてみます。  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p  
    SELECT * FROM t WHERE c1 > @p  
    ```  
  
     最初のケースでは、このトピックで前述したルールに従って、型推論アルゴリズム推測**char (30)** を \@p のデータ型として使用します。 2番目のケースでは、次のセクションの一般的な推論規則に従って、型推論アルゴリズム推測**varchar (8000)** になります。  
  
-   一般的な推論  
  
     単純な推論が適用されない場合、宣言されていないパラメーターのデータ型は次のように見なされます。  
  
    -   整数データ型 (**bit**、 **tinyint**、 **smallint**、 **int**、 **bigint**)  
  
    -   Money データ型 (**smallmoney**、 **money**)  
  
    -   浮動小数点データ型 (**float**、 **real**)  
  
    -   **numeric (38, 19)** -その他の数値または decimal データ型は考慮されません。  
  
    -   **varchar (8000)** 、 **varchar (max)** 、 **nvarchar (4000)** 、および**nvarchar (max)** -その他の文字列データ型 ( **text**、 **char (8000)** 、 **nvarchar (30)** など) は考慮されません。  
  
    -   **varbinary (8000)** と**varbinary (max)** -その他のバイナリデータ型は考慮されません ( **image**、 **binary (8000)** 、 **varbinary (30)** など)。  
  
    -   **date**、 **time (7)** 、 **smalldatetime**、 **datetime**、 **datetime2 (7)** 、 **datetimeoffset (7)** -その他の日付/時刻型 ( **time (4) など)** は考慮されません。  
  
    -   **sql_variant**  
  
    -   **xml**  
  
    -   CLR システム定義型 (**hierarchyid**、 **geometry**、 **geography**)  
  
    -   CLR ユーザー定義型  
  
### <a name="selection-criteria"></a>選択条件  
 候補のデータ型のうち、クエリを無効にするデータ型は拒否されます。 残りの候補のデータ型の場合、型推論アルゴリズムは次の規則に従って1つを選択します。  
  
1.  E (\@p) での暗黙的な変換の最小数を生成するデータ型が選択されています。 特定のデータ型によって、TT (\@p) とは異なる E (\@p) のデータ型が生成された場合、型推論アルゴリズムは、これを E (\@p) のデータ型から TT (\@p) への追加の暗黙的な変換と見なします。  
  
     例 :  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_Int + @p  
    ```  
  
     この場合、E (\@p) は Col_Int + \@p であり、TT (\@p) は**Int**です。暗黙的な変換が生成されないため、\@p に対して**int**が選択されています。 その他の任意のデータ型では、少なくとも1つの暗黙的な変換が生成されます。  
  
2.  変換の最小数に対して複数のデータ型が関連付けられている場合は、優先順位の高いデータ型が使用されます。 次に例を示します。  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_smallint + @p  
    ```  
  
     この場合、 **int**と**smallint**は1つの変換を生成します。 他のすべてのデータ型では、2 つ以上の変換が生成されます。 **Int**は**smallint**よりも優先されるため、\@p には**int**が使用されます。 データ型の優先順位の詳細については、「[データ型&#41;の優先順位&#40;transact-sql](../../t-sql/data-types/data-type-precedence-transact-sql.md)」を参照してください。  
  
     このルールは、ルール 1 に該当するすべてのデータ型と、最高位の優先順位を持つデータ型との間に暗黙的な変換がある場合にのみ適用されます。 暗黙的な変換がない場合、データ型の推論はエラーで失敗します。 たとえば、クエリ `SELECT @p FROM t`では、\@p の任意のデータ型が同等に適しているため、データ型の推論は失敗します。 たとえば、int から**xml**への暗黙の**型**変換はありません。  
  
3.  2つの類似したデータ型が rule 1 に関連付けられている場合 ( **varchar (8000)** と**varchar (max)** など) は、小さい方のデータ型 (**varchar (8000)** ) が選択されます。 **Nvarchar**および**varbinary**データ型にも同じ原則が適用されます。  
  
4.  ルール 1 のために、型推論アルゴリズムでは、特定の変換が他の変換よりも優先されます。 変換の優先順序は、次のとおりです。  

    1.  異なる長さの同じ基本データ型間の変換。  
  
    2.  同じデータ型の固定長と可変長のバージョン ( **char**から**varchar**など) の間の変換。  
  
    3.  **NULL**と**int**の間の変換です。  
  
    4.  その他の変換。  
  
 たとえば、クエリ `SELECT * FROM t WHERE [Col_varchar(30)] > @p`では、変換 (a) が最適であるため、 **varchar (8000)** が選択されています。 クエリ `SELECT * FROM t WHERE [Col_char(30)] > @p`では、 **varchar (8000)** が引き続き選択されます。これは、型 (b) 変換が発生し、別の選択肢 ( **varchar (4000)** など) によって型 (d) が変換されるためです。  
  
 最後の例として、クエリ `SELECT NULL + @p`を指定した場合は、int が型 (c) に変換されるため、\@p に対して**int**が選択されます。  
  
## <a name="permissions"></a>アクセス許可  
 \@tsql 引数を実行する権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、宣言されていない `@id` パラメーターおよび `@name` パラメーターに対して予期されるデータ型などの情報を返します。  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR name = @name'  
  
```  
  
 `@id` パラメーターが `@params` 参照として指定された場合は、`@id` パラメーターは結果セットから省略され、`@name` パラメーターのみが記述されます。  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR NAME = @name',  
@params = N'@id int'  
  
```  
  
## <a name="see-also"></a>参照  
 [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [dm_exec_describe_first_result_set &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)
