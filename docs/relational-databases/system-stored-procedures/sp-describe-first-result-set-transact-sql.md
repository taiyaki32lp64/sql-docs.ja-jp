---
title: sp_describe_first_result_set (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc58447e9893647dfa73643f14455d715625478e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053050"
---
# <a name="spdescribefirstresultset-transact-sql"></a>sp_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  最初の考えられる結果セットのメタデータを返します、[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチ。 バッチに結果が返されない場合は、設定、空の結果を返します。 エラーが発生、[!INCLUDE[ssDE](../../includes/ssde-md.md)]静的分析を実行することによって実行される最初のクエリのメタデータを判断することはできません。 動的管理ビュー [sys.dm_exec_describe_first_result_set &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)同じ情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>引数  
`[ \@tsql = ] 'Transact-SQL_batch'` 1 つまたは複数[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。 *Transact SQL_batch*あります**nvarchar (***n***)** または**nvarchar (max)** します。  
  
`[ \@params = ] N'parameters'` \@params パラメーターの宣言文字列の提供、[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチは、これは、sp_executesql と同様にします。 パラメーターがあります**nvarchar (n)** または**nvarchar (max)** します。  
  
 1 つの文字列に埋め込まれたすべてのパラメーターの定義を含む、 [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*します。 この文字列は Unicode 定数または Unicode 変数にする必要があります。 各パラメーター定義は、パラメーター名とデータ型で構成されます。 *n*は追加のパラメーター定義を示すプレース ホルダーです。 ステートメントで指定されたすべてのパラメーターを定義する必要があります\@params します。 場合、[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントまたはステートメント内のバッチは、パラメーターを含まない\@params は必要ありません。 NULL は、このパラメーターの既定値です。  
  
`[ \@browse_information_mode = ] tinyint` 追加のキー列とソース テーブル情報が返されるかどうかを指定します。 場合は、クエリに FOR BROWSE オプションが含まれている場合に、1、各クエリに設定するが分析されます。 追加のキー列とソース テーブル情報が返されます。  
  
-   かどうかは 0 に設定すると、情報は返されません。  
  
-   場合は、クエリに FOR BROWSE オプションが含まれている場合に、1、各クエリに設定するが分析されます。 ベースのテーブル名がソース列情報として返されます。  
  
-   かどうかは 2 に設定すると、各クエリはように分析は、準備またはカーソルを実行中で使用されます。 ビュー名がソース列情報として返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **sp_describe_first_result_set**常に成功した場合に 0 の状態を返します。 プロシージャは、エラーをスローします。 プロシージャが RPC として呼び出された場合は、状態の戻り値は sys.dm_exec_describe_first_result_set の error_type 列に記述されているエラーの種類が設定されます。 プロシージャが呼び出された場合[!INCLUDE[tsql](../../includes/tsql-md.md)]、戻り値は常に 0、エラーがある場合でもです。  
  
## <a name="result-sets"></a>結果セット  
 この共通メタデータは、結果のメタデータの各列に対する 1 行の結果セットとして返されます。 各行には、列の種類と NULL 値の許容属性が次のセクションに示す形式で記述されます。 最初のステートメントは、各コントロールのパスが存在しない場合は、0 行を含む結果セットが返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit NOT NULL**|列が、参照情報のために追加された追加の列であると、それが表示されないこと実際に結果セットを示します。|  
|**column_ordinal**|**int NOT NULL**|結果セット内の列の位置を示す序数を格納します。 最初の列の位置は 1 として指定されます。|  
|**name**|**sysname NULL**|列の名前を確認できる場合は、その名前を格納します。 それ以外の場合、NULL が含まれます。|  
|**is_nullable**|**bit NOT NULL**|列は Null を許可する場合に特定できない場合に、Null を列に Null を許容しない場合は 0 と 1 を許可する場合は、値 1 が含まれています。|  
|**system_type_id**|**int NOT NULL**|Sys.types で指定された列のデータ型の system_type_id を格納します。 CLR 型の場合は、system_type_name 列が NULL を返しても、この列は値 240 を返します。|  
|**system_type_name**|**nvarchar(256) NULL**|列のデータ型に指定されている名前と引数 (長さ、有効桁数、小数点以下桁数など) を格納します。 データ型がユーザー定義の別名型の場合は、基になるシステム型がここで指定されます。 CLR ユーザー定義型の場合は、この列には NULL が返されます。|  
|**max_length**|**smallint NOT NULL**|列の最大長 (バイト単位) です。<br /><br /> -1 = 列のデータ型は**varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、または**xml**します。<br /><br /> **テキスト**、列、 **max_length**値は 16 かによって設定された値になります**sp_tableoption 'text in row'** します。|  
|**有効桁数 (precision)**|**tinyint NOT NULL**|数値ベースの場合は、列の有効桁数です。 それ以外の場合 0 を返します。|  
|**scale**|**tinyint NOT NULL**|数値ベースの場合は、列の小数点以下桁数です。 それ以外の場合 0 を返します。|  
|**collation_name**|**sysname NULL**|文字ベースの場合は、列の照合順序の名前です。 それ以外の場合、NULL を返します。|  
|**user_type_id**|**int NULL**|CLR 型と別名型の場合、sys.types で指定された列のデータ型の user_type_id を格納します。 それ以外の場合は NULL です。|  
|**user_type_database**|**sysname NULL**|CLR 型と別名型の場合、その型が定義されたデータベースの名前を格納します。 それ以外の場合は NULL です。|  
|**user_type_schema**|**sysname NULL**|CLR 型と別名型の場合、その型が定義されたスキーマの名前を格納します。 それ以外の場合は NULL です。|  
|**user_type_name**|**sysname NULL**|CLR 型と別名型の場合、その型の名前を格納します。 それ以外の場合は NULL です。|  
|**assembly_qualified_type_name**|**nvarchar (4000)**|CLR 型の場合、その型を定義するアセンブリの名前とクラスを返します。 それ以外の場合は NULL です。|  
|**xml_collection_id**|**int NULL**|sys.columns で指定された列のデータ型の xml_collection_id を格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**xml_collection_database**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションが定義されているデータベースを格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**xml_collection_schema**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションが定義されているスキーマを格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**xml_collection_name**|**sysname NULL**|この型に関連付けられている XML スキーマ コレクションの名前を格納します。 この列は、返される型が XML スキーマ コレクションに関連付けられていない場合は NULL を返します。|  
|**is_xml_document**|**bit NOT NULL**|返されたデータ型が XML で、その型が XML フラグメントではなく完全な XML ドキュメント (ルート ノードを含む) であると保証される場合、1 を返します。 それ以外の場合 0 を返します。|  
|**is_case_sensitive**|**bit NOT NULL**|されていない場合、列が大文字の文字列型で、0 の場合は、1 を返します。|  
|**is_fixed_length_clr_type**|**bit NOT NULL**|されていない場合、列が固定長の CLR 型と 0 の場合は、1 を返します。|  
|**source_server**|**sysname**|この結果内の列によって返された元のサーバーの名前です (リモート サーバーから発生する場合)。 Sys.servers に表示される、名前が与えられます。 この列がローカル サーバー上で発生した場合、または元のサーバーを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_database**|**sysname**|この結果内の列によって返された元のデータベースの名前です。 データベースを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_schema**|**sysname**|この結果内の列によって返された元のスキーマの名前です。 スキーマを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_table**|**sysname**|この結果内の列によって返された元のテーブルの名前です。 テーブルを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_column**|**sysname**|結果列から返された元の列の名前です。 列を特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**is_identity_column**|**bit NULL**|この列が ID 列の場合は 1、それ以外の場合は 0 を返します。 ID 列であることを確認できない場合は NULL を返します。|  
|**is_part_of_unique_key**|**bit NULL**|この列が一意インデックス (一意制約と主キー制約を含む) の一部である場合は 1、それ以外の場合は 0 を返します。 一意インデックスの一部であることを確認できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**is_updateable**|**bit NULL**|この列が更新可能である場合は 1、それ以外の場合は 0 を返します。 更新可能であることを確認できない場合は NULL を返します。|  
|**is_computed_column**|**bit NULL**|この列が計算列の場合は 1、それ以外の場合は 0 を返します。 列が計算列を特定できない場合は、NULL を返します。|  
|**is_sparse_column_set**|**bit NULL**|この列がスパース列の場合は 1、それ以外の場合は 0 を返します。 列がスパース列セットの一部であることを特定できない場合は、NULL を返します。|  
|**ordinal_in_order_by_list**|**smallint NULL**|ORDER BY リストにおけるこの列の位置。 列が ORDER BY リストに表示されない場合、または ORDER BY リストを一意に特定できない場合は、NULL を返します。|  
|**order_by_list_length**|**smallint NULL**|ORDER BY リストの長さを返します。 ORDER BY リストがない場合、または ORDER BY リストを一意に特定できない場合は NULL を返します。 この値がによって返されるすべての行で同じになることに注意してください。 **sp_describe_first_result_set します。**|  
|**order_by_is_descending**|**smallint NULL**|Ordinal_in_order_by_list が NULL でない場合、 **order_by_is_descending**列は、この列の ORDER BY 句の方向を報告します。 それ以外の場合は、NULL が報告されます。|  
|**tds_type_id**|**int NOT NULL**|内部使用です。|  
|**tds_length**|**int NOT NULL**|内部使用です。|  
|**tds_collation_id**|**int NULL**|内部使用です。|  
|**tds_collation_sort_id**|**tinyint NULL**|内部使用です。|  
  
## <a name="remarks"></a>コメント  
 **sp_describe_first_result_set**こと、プロシージャが (仮定) の最初の結果セットのメタデータを返す場合バッチ A と、そのバッチ (A) が、その後実行し、バッチの保証は (1) 最適化時エラーを発生させます (2)発生させ、実行時のエラー (3) 返します結果はありませんセット、または (4) で説明されている同じメタデータを持つ最初の結果が設定**sp_describe_first_result_set**します。  
  
 名前、NULL 値の許容属性、およびデータ型が異なる可能性があります。 場合**sp_describe_first_result_set**バッチ実行の結果セットが返される保証は、空の結果セットを返します。  
  
 この保証では、サーバーに関連するスキーマの変更がないと仮定します。 サーバーに関連するスキーマ変更したりしないでください一時テーブルの作成は、テーブル間のバッチ A で変数を**sp_describe_first_result_set**呼びますと中に返される結果セット時刻B. バッチによるスキーマ変更をなどの実行  
  
 **sp_describe_first_result_set**場合は、次のいずれかでエラーが返されます。  
  
-   場合、入力\@tsql が有効ではありません[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチ。 有効性は、解析および分析によって決まりますが、[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチ。 クエリの最適化中または実行中に、バッチによるエラーは、決定する際に考慮されないかどうか、[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチが有効です。  
  
-   場合\@1 回以上のパラメーターを宣言する文字列が含まれている場合、またはパラメーターが NULL でないと、パラメーターの宣言の構文が有効な文字列でない文字列が含まれています。  
  
-   場合、入力[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチで宣言されているパラメーターに同じ名前のローカル変数を宣言します\@params します。  
  
-   場合は、ステートメントは、一時テーブルを使用します。  
  
-   クエリには、クエリを実行し、永続的なテーブルの作成が含まれています。  
  
 その他のすべてのチェックが成功した場合、入力バッチ内のすべての制御フロー パスと見なされます。 このを考慮に入れたすべての制御フロー ステートメント (GOTO、IF/ELSE、WHILE、および[!INCLUDE[tsql](../../includes/tsql-md.md)]TRY/CATCH ブロック)、プロシージャは、動的と[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチ、または EXEC ステートメント、DDL ステートメントをして入力バッチから呼び出されたトリガー発生させる DDL トリガーまたは対象のテーブルまたはテーブルが外部キー制約のカスケード操作により変更されるトリガーを起動する DML ステートメント。 多くの可能なコントロール パスの場合はある時点でアルゴリズムを停止します。  
  
 各制御フロー パスの最初のステートメント (あれば) を返す結果セットが続く**sp_describe_first_result_set**します。  
  
 複数の使用可能な最初のステートメントがバッチ内で見つかったときにその結果できます列、列名、null 許容属性、およびデータ型の数が異なります。 これらの違いを処理する方法の詳細について、ここに記載します。  
  
-   列の数が異なる場合は、エラーがスローされ、結果は返されません。  
  
-   列名が異なる場合は、返される列名が NULL に設定されます。  
  
-   Null 値の許容とは異なること返される null 値許容属性が Null を許容します。  
  
-   データ型が異なる場合は、エラーがスローされ、次の場合を除いて結果は返されません。  
  
    -   **varchar (a)** に**varchar(a')** 場所、' > をします。  
  
    -   **varchar (a)** に**varchar (max)**  
  
    -   **nvarchar (a)** に**nvarchar(a')** 場所、' > をします。  
  
    -   **nvarchar (a)** に**nvarchar (max)**  
  
    -   **varbinary (a)** に**varbinary(a')** 場所、' > をします。  
  
    -   **varbinary (a)** に**varbinary (max)**  
  
 **sp_describe_first_result_set**は間接再帰をサポートしていません。  
  
## <a name="permissions"></a>アクセス許可  
 実行する権限が必要です、 \@tsql 引数。  
  
## <a name="examples"></a>使用例  
  
### <a name="typical-examples"></a>一般的な例  
  
#### <a name="a-simple-example"></a>A. 簡単な例  
 次の例では、1 つのクエリから返される結果について説明します。  
  
```  
sp_describe_first_result_set @tsql = N'SELECT object_id, name, type_desc FROM sys.indexes'  
```  
  
 次の例では、パラメーターを含む 1 つのクエリから返される結果を示します。  
  
```  
sp_describe_first_result_set @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes   
WHERE object_id = @id1'  
, @params = N'@id1 int'  
```  
  
#### <a name="b-browse-mode-examples"></a>B. ブラウズ モードの使用例  
 次の 3 つの例では、異なるブラウズ情報モード間の主要な違いを示します。 クエリ結果には、関係する列だけが含まれています。  
  
 情報がないことを示します。 0 の使用例が返されます。  
  
```sql  
CREATE TABLE dbo.t (a int PRIMARY KEY, b1 int);  
GO  
CREATE VIEW dbo.v AS SELECT b1 AS b2 FROM dbo.t;  
GO  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM dbo.v', null, 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|NAME|source_schema|ソース テーブル|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|NULL|NULL|NULL|NULL|  
  
 1 示すを使用した例は、クエリに FOR BROWSE オプションが含まれている場合、情報を返します。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|NAME|source_schema|ソース テーブル|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|dbo|t|B1|0|  
|1|2|a|dbo|t|a|1|  
  
 カーソルを準備する場合、分析対象を示す 2 を使用する例です。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|NAME|source_schema|ソース テーブル|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|B3|dbo|v|B2|0|  
|1|2|ROWSTAT|NULL|NULL|NULL|0|  
  
### <a name="examples-of-problems"></a>問題の例  
 以下の例では、すべて 2 つのテーブルを使用します。 次のステートメントを実行して、これらのテーブルを作成します。  
  
```  
CREATE TABLE dbo.t1 (a int NULL, b varchar(10) NULL, c nvarchar(10) NULL);  
CREATE TABLE dbo.t2 (a smallint NOT NULL, d varchar(20) NOT NULL, e int NOT NULL);  
```  
  
#### <a name="error-because-the-number-of-columns-differ"></a>列の数の違いによるエラー  
 この例では最初の結果セットが異なるできるだけの列の数。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a, b FROM t1;  
SELECT * FROM t; -- Ignored, not a possible first result set.'  
  
```  
  
#### <a name="error-because-the-data-types-differ"></a>データ型の違いによるエラー  
 考えられる最初の結果セットの間で、列の型が異なります。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a FROM t2;  
```  
  
 結果:エラー、型の不一致 (**int**と**smallint**)。  
  
#### <a name="column-name-cannot-be-determined"></a>列名を確認することはできません。  
 可能な最初の結果セットが異なる同じ可変長型、null 許容属性、および列名の長さの列:  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d FROM t2; '  
```  
  
 結果:\<不明な列名 > **varchar (20) NULL**  
  
#### <a name="column-name-forced-to-be-identical-through-aliasing"></a>別名の指定と同じでなければ強制的に列名  
 前の例と同じですが、列の別名を使用して列名を同じにしています。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d AS b FROM t2;'  
```  
  
 Result: b **varchar(20)NULL**  
  
#### <a name="error-because-column-types-cannot-be-matched"></a>エラー列の型が一致することはできませんので、  
 考えられる、異なる列の型が異なる最初の結果セット。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT c FROM t1;'  
```  
  
 結果:エラー、型の不一致 (**varchar (10)** と**nvarchar (10)** )。  
  
#### <a name="result-set-can-return-an-error"></a>結果セットはエラーを返すことができます。  
 最初の結果セットはエラーまたは結果セットです。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RAISERROR(''Some Error'', 16, 1);  
  
ELSE  
    SELECT a FROM t1;  
SELECT e FROM t2; -- Ignored, not a possible first result set.;'  
```  
  
 結果: **intNULL**  
  
#### <a name="some-code-paths-return-no-results"></a>一部のコード パスに結果が返されない  
 最初の結果セットが null または結果セットです。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 結果: **intNULL**  
  
#### <a name="result-from-dynamic-sql"></a>動的 SQL からの結果します。  
 最初の結果セットは、リテラル文字列であるために、探索可能な動的 SQL です。  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 結果: **INT NULL**  
  
#### <a name="result-failure-from-dynamic-sql"></a>動的 SQL からの結果の失敗  
 動的 SQL のため、最初の結果セットが未定義となります。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL); '  
```  
  
 結果:エラー状態。 動的 SQL のため結果を検出できません。  
  
#### <a name="result-set-specified-by-user"></a>ユーザー指定の結果セット  
 最初の結果セットがユーザーにより手動で指定されています。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL)  
    WITH RESULT SETS(  
        (Column1 BIGINT NOT NULL)  
    ); '  
```  
  
 結果:Column1 **bigint NOT NULL**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>あいまいな結果セットによるエラー  
 この例では、user1 という名前の別のユーザーが列を含む既定のスキーマ s1 内の t1 という名前のテーブル (、 **int NOT NULL**)。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 結果:エラー状態。 t1 は dbo.t1 または s1.t1、それぞれ異なる数の列のいずれかを指定できます。  
  
#### <a name="result-even-with-ambiguous-result-set"></a>あいまいな結果セットを使用しても結果します。  
 前の例と同じ前提を使用します。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 結果: **int NULL** dbo.t1.a と s1.t1.a 型であるため、 **int**と異なる null 許容属性。  
  
## <a name="see-also"></a>関連項目  
 [sp_describe_undeclared_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
 
