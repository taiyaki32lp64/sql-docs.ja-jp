---
title: sp_execute_external_script (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: ab3bf4f98abaf5f164a3b38f4e09b10acf28b2f4
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532830"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**Sp_execute_external_script**ストアドプロシージャは、プロシージャへの入力引数として指定されたスクリプトを実行し、 [Machine Learning Services](../../advanced-analytics/index.yml)および[言語拡張](../../language-extensions/language-extensions-overview.md)と共に使用されます。 

Machine Learning Services の場合、 [Python](../../advanced-analytics/concepts/extension-python.md)と[R](../../advanced-analytics/concepts/extension-r.md)はサポートされている言語です。 言語拡張の場合、Java はサポートされていますが、 [CREATE EXTERNAL Language](../../t-sql/statements/create-external-language-transact-sql.md)を使用して定義する必要があります。

**Sp_execute_external_script**を実行するには、最初に Machine Learning Services または言語拡張機能をインストールする必要があります。 詳細については、Windows および[linux](../../linux/sql-server-linux-setup-machine-learning.md)[に SQL Server Machine Learning Services (Python および R) をインストール](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md)するか、windows および[Linux](../../linux/sql-server-linux-setup-language-extensions.md)[に SQL Server 言語拡張機能をインストール](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md)してください。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**Sp_execute_external_script**ストアドプロシージャは、プロシージャへの入力引数として指定されたスクリプトを実行し、SQL Server 2017 の[Machine Learning Services](../../advanced-analytics/index.yml)と共に使用します。 

Machine Learning Services の場合、 [Python](../../advanced-analytics/concepts/extension-python.md)と[R](../../advanced-analytics/concepts/extension-r.md)はサポートされている言語です。 

**Sp_execute_external_script**を実行するには、最初に Machine Learning Services をインストールする必要があります。 詳細については、「 [Install SQL Server Machine Learning Services (Python および R) On Windows](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md)」を参照してください。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Sp_execute_external_script**ストアドプロシージャは、プロシージャへの入力引数として指定されたスクリプトを実行し、SQL Server 2016 の[R Services](../../advanced-analytics/r/sql-server-r-services.md)と共に使用します。

R Services の場合、サポートされている言語は[r](../../advanced-analytics/concepts/extension-r.md)です。

**Sp_execute_external_script**を実行するには、最初に R Services をインストールする必要があります。 詳細については、「 [Install SQL Server Machine Learning Services (Python および R) On Windows](../../advanced-analytics/install/sql-r-services-windows-install.md)」を参照してください。
::: moniker-end

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax"></a>構文

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]    
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>2017以前の構文

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>引数
 **\@言語**= N '*language*'  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 スクリプト言語を示します。 *言語*は**sysname**です。 有効な値は、 **R**、 **Python**、および[CREATE EXTERNAL language](../../t-sql/statements/create-external-language-transact-sql.md) (Java など) で定義されている任意の言語です。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 スクリプト言語を示します。 *言語*は**sysname**です。 SQL Server 2017 では、有効な値は**R**および**Python**です。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 スクリプト言語を示します。 *言語*は**sysname**です。 SQL Server 2016 では、有効な値は**R**のみです。
::: moniker-end

 **\@スクリプト**= N '*script*' 外部言語スクリプトがリテラルまたは変数入力として指定されています。 *スクリプト*は**nvarchar (max)** です。  

`[ @input_data_1 =  N'input_data_1' ]` [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリの形式で外部スクリプトによって使用される入力データを指定します。 *Input_data_1*のデータ型は**nvarchar (max)** です。

`[ @input_data_1_name = N'input_data_1_name' ]` @input_data_1によって定義されたクエリを表すために使用する変数の名前を指定します。 外部スクリプトの変数のデータ型は、言語によって異なります。 R の場合、入力変数はデータフレームです。 Python の場合、入力は表形式である必要があります。 *input_data_1_name*は**sysname**です。  既定値は*Inputdataset*です。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`、パーティションごとのモデルを構築するために使用されます。 結果セットの順序付けに使用する列の名前を指定します。たとえば、製品名を使用します。 外部スクリプトの変数のデータ型は、言語によって異なります。 R の場合、入力変数はデータフレームです。 Python の場合、入力は表形式である必要があります。

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`、パーティションごとのモデルを構築するために使用されます。 地理的領域や日付など、データのセグメント化に使用する列の名前を指定します。 外部スクリプトの変数のデータ型は、言語によって異なります。 R の場合、入力変数はデータフレームです。 Python の場合、入力は表形式である必要があります。 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` は、ストアドプロシージャの呼び出しの完了時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に返されるデータを含む外部スクリプト内の変数の名前を指定します。 外部スクリプトの変数のデータ型は、言語によって異なります。 R の場合、出力はデータフレームである必要があります。 Python の場合、出力はパンダのデータフレームである必要があります。 *output_data_1_name*は**sysname**です。  既定値は*Outputdataset*です。  

`[ @parallel = 0 | 1 ]` `@parallel` パラメーターを1に設定することにより、R スクリプトの並列実行を有効にします。 このパラメーターの既定値は 0 (並列処理なし) です。 `@parallel = 1` と出力がクライアントコンピューターに直接ストリーミングされている場合は、`WITH RESULT SETS` 句が必要であり、出力スキーマを指定する必要があります。  

 + RevoScaleR 関数を使用しない R スクリプトの場合は、スクリプトを事前に並列化できると仮定して、`@parallel` パラメーターを使用すると、大規模なデータセットを処理するのに役立ちます。 たとえば、R `predict` 関数をモデルと共に使用して新しい予測を生成する場合は、クエリエンジンへのヒントとして `@parallel = 1` を設定します。 クエリを並列化できる場合、行は**MAXDOP**の設定に従って分散されます。  
  
 + RevoScaleR functions を使用する R スクリプトの場合、並列処理は自動的に処理されるので、 **sp_execute_external_script**呼び出しに `@parallel = 1` を指定しないでください。  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` 外部スクリプトで使用される入力パラメーター宣言の一覧。  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` 外部スクリプトで使用される入力パラメーターの値の一覧です。  

## <a name="remarks"></a>解説

> [!IMPORTANT]
> クエリツリーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって制御され、ユーザーはクエリに対して任意の操作を実行できません。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**Sp_execute_external_script**を使用して、サポートされている言語で記述されたスクリプトを実行します。 サポートされている言語は、Machine Learning Services で使用される**Python**と**R** 、および言語拡張機能で使用される[CREATE EXTERNAL language](../../t-sql/statements/create-external-language-transact-sql.md) (Java など) で定義されているすべての言語です。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**Sp_execute_external_script**を使用して、サポートされている言語で記述されたスクリプトを実行します。 サポートされている言語は SQL Server 2017 Machine Learning Services の**Python**および**R**です。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Sp_execute_external_script**を使用して、サポートされている言語で記述されたスクリプトを実行します。 サポートされている言語は SQL Server 2016 R Services の**r**のみです。
::: moniker-end

既定では、このストアドプロシージャによって返される結果セットには、名前のない列が出力されます。 スクリプト内で使用される列名は、スクリプト環境に対してローカルであり、出力される結果セットには反映されません。 結果セット列の名前を指定するには、 [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)の `WITH RESULT SET` 句を使用します。

結果セットを返すだけでなく、出力パラメーターを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にスカラー値を返すことができます。 
  
外部リソースプールを構成することによって、外部スクリプトによって使用されるリソースを制御できます。 詳細については、「[CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)」を参照してください。 ワークロードに関する情報は、リソースガバナーのカタログビュー、DMV の、およびカウンターから取得できます。 詳細については、「 [Resource Governor &#40;カタログビュー transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)」、「 [Resource Governor 関連する&#40;動的管理ビュー&#41;transact-sql](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)」、および「 [SQL Server External Scripts オブジェクト](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)」を参照してください。  

### <a name="monitor-script-execution"></a>スクリプトの実行の監視

スクリプトの実行を監視するには、 [(または](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)、[要求](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)を実行してください。) 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>パーティションモデリングのパラメーター

パーティション分割されたデータでのモデリングを可能にする2つの追加パラメーターを設定できます。この場合、パーティションは、指定した1つ以上の列に基づいて作成され、スクリプトの実行中にのみ使用される論理パーティションにデータセットを分割します。 年齢、性別、地域、日付、または時刻の繰り返し値を含む列は、パーティション分割されたデータセットに適したいくつかの例です。
 
2つのパラメーター **input_data_1_partition_by_columns**と**input_data_1_order_by_columns**は、2番目のパラメーターを使用して結果セットを並べ替えます。 パラメーターは `sp_execute_external_script` に入力として渡され、外部スクリプトは各パーティションに対して1回実行されます。 詳細と例については、「[チュートリアル: パーティションベースのモデルを作成する](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition)」を参照してください。

`@parallel=1`を指定することにより、スクリプトを並列実行できます。 入力クエリを並列化できる場合は、引数の一部として `@parallel=1` を `sp_execute_external_script` に設定する必要があります。 既定では、クエリオプティマイザーは、256行を超えるテーブルの `@parallel=1` 下で動作しますが、これを明示的に処理する場合、このスクリプトにはパラメーターがデモンストレーションとして含まれます。

> [!Tip]
> トレーニング作業については、Microsoft rx 以外のアルゴリズムを使用している場合でも、任意のトレーニングスクリプトで `@parallel` を使用できます。 通常、SQL Server のトレーニングシナリオでは、RevoScaleR アルゴリズム (rx プレフィックスを持つ) のみが並列処理を提供します。 ただし、SQL Server vNext の新しいパラメーターを使用すると、その機能を使用して特に設計されていない関数を呼び出すスクリプトを並列化できます。
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Python および R スクリプトのストリーミング実行  

ストリーミングを使用すると、Python または R スクリプトは、メモリに収まりきらないデータを処理できます。 ストリーミング中に渡される行の数を制御するには、パラメーターに整数値を指定し、`@params` コレクションには `@r_rowsPerRead` を指定します。  たとえば、非常に幅の広いデータを使用するモデルをトレーニングする場合、1つのデータチャンクですべての行を確実に送信できるようにするために、値を小さくして読み取る行を減らすことができます。 また、このパラメーターを使用して、サーバーのパフォーマンスの問題を軽減するために、一度に読み取られて処理される行の数を管理することもできます。 
  
Streaming の `@r_rowsPerRead` パラメーターと `@parallel` 引数の両方をヒントと見なす必要があります。 ヒントを適用するには、並列処理を含む SQL クエリプランを生成できる必要があります。 これが不可能な場合は、並列処理を有効にできません。  
  
> [!NOTE]  
> ストリーミングと並列処理は、Enterprise Edition でのみサポートされています。 標準エディションのクエリには、エラーを発生させることなくパラメーターを含めることができますが、パラメーターが無効になり、R スクリプトが1つのプロセスで実行されます。  
  
## <a name="restrictions"></a>制限  

### <a name="data-types"></a>データ型

次のデータ型は、 **sp_execute_external_script**プロシージャの入力クエリまたはパラメーターで使用する場合はサポートされていません。また、サポートされていない型エラーを返します。  

回避策として、列または値を [!INCLUDE[tsql](../../includes/tsql-md.md)] のサポートされている型に**キャスト**してから、外部スクリプトに送信します。  
  
-   **カーソル (cursor)**  
  
-   **timestamp**  
  
-   **datetime2**、 **datetimeoffset**、 **time**  
  
-   **sql_variant**  
  
-   **text**、 **image**  
  
-   **xml**  
  
-   **hierarchyid**、 **geometry**、 **geography**  
  
-   CLR ユーザー定義型

一般に、[!INCLUDE[tsql](../../includes/tsql-md.md)] データ型にマップできない結果セットは、NULL として出力されます。  

### <a name="restrictions-specific-to-r"></a>R に固有の制限事項

入力に、R の許容範囲の値に適合しない**datetime**値が含まれている場合、値は**NA**に変換されます。 これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が R 言語でサポートされているよりも大きな値の範囲を許可するために必要です。

両方の言語で IEEE 754 が使用されている場合でも、Float 値 (たとえば、`+Inf`、`-Inf`、`NaN`) は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではサポートされません。 現在の動作では、値が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に直接送信されます。その結果、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の SQL クライアントがエラーをスローします。 そのため、これらの値は**NULL**に変換されます。

## <a name="permissions"></a>アクセス許可

**すべての外部スクリプトデータベースの実行**権限が必要です。  

## <a name="examples"></a>使用例

このセクションでは、このストアドプロシージャを使用して、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して R または Python スクリプトを実行する方法の例について説明します。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. R データセットを SQL Server に返す  

次の例では、 **sp_execute_external_script**を使用して、R に含まれる虹彩データセットを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に返すストアドプロシージャを作成します。  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. SQL Server からのデータに基づいて R モデルを生成する  

次の例では、 **sp_execute_external_script**を使用して、虹彩モデルを生成し、モデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に返すストアドプロシージャを作成します。  

> [!NOTE]
>  この例では、e1071 パッケージを事前にインストールする必要があります。 詳細については、「 [SQL Server に追加の R パッケージをインストール](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)する」を参照してください。

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

Python を使って似たモデルを生成するには、言語識別子を `@language=N'R'` から `@language = N'Python'` に変更し、`@script` 引数を必要に応じて修正します。 そうしないと、すべてのパラメーターが R と同じように機能します。

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Python モデルを作成し、そこからスコアを生成する

この例では、\_execute\_external\_script を使って簡単な Python モデルでスコアを生成する方法を示します。 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Python コードで使用される列見出しは SQL Server に出力されません。したがって、SQL で使用する列の名前とデータ型を指定するには、WITH RESULT ステートメントを使用します。

スコアリングには、ネイティブな [PREDICT](../../t-sql/queries/predict-transact-sql.md) 関数を使うこともできます。通常、これは Python や R のランタイムを呼び出さないので高速です。

## <a name="see-also"></a>参照

+ [SQL Server Machine Learning Services](../../advanced-analytics/index.yml)
+ [SQL Server 言語拡張機能](../../language-extensions/language-extensions-overview.md)。 
+ [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Python ライブラリとデータ型](../../advanced-analytics/python/python-libraries-and-data-types.md)  
+ [R ライブラリと R データ型](../../advanced-analytics/r/r-libraries-and-data-types.md)  
+ [SQL Server R サービス](../../advanced-analytics/r/sql-server-r-services.md)   
+ [SQL Server Machine Learning Services に関する既知の問題](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
+ [CREATE EXTERNAL LIBRARY &#40;transact-sql&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [external scripts enabled サーバー構成オプション](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server のExternal Scripts オブジェクト](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
