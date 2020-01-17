---
title: sqlrutils ヘルパー関数
description: SQL Server 2016 R Services および SQL Server Machine Learning Services (R 付属) の sqlrutils 関数ライブラリを使用して、R スクリプトを含むストアド プロシージャを生成します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3de8d438691afb7ebf1aabe15265227b7876b837
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715029"
---
# <a name="sqlrutils-r-library-in-sql-server"></a>sqlrutils (SQL Server の R ライブラリ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**sqlrutils** パッケージは R ユーザーに、R スクリプトを T-SQL ストアド プロシージャに配置し、そのストアド プロシージャをデータベースに登録し、R 開発環境からそのストアド プロシージャを実行するメカニズムを提供します。 

R コードを変換して 1 つのストアド プロシージャ内で実行されるようにすると、R スクリプトが [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)へのパラメーターとして埋め込まれる必要のある SQL Server R Services をより効率的に使用できるようになります。 **sqlrutils** パッケージを使用すると、この組み込みの R スクリプトを構築し、関連するパラメーターを適切に設定することができます。

**sqlrutils** パッケージは、次を行います。

- 生成された T-SQL スクリプトを R データ構造内に文字列として保存する
- オプションで、ストアド プロシージャを編集または実行できる .sql ファイルを T-SQL スクリプト用に生成する
- 新しく作成したストアド プロシージャを R 開発環境から SQL Server インスタンスに登録できる

整形されたパラメーターを渡し、結果を処理することによって、R 環境からストアド プロシージャを実行することも可能です。 または、ETL、モデルのトレーニング、大量のスコア付けなどの一般的なデータベースの統合シナリオをサポートするよう、SQL Server からストアド プロシージャを使用することも可能です。

  > [!NOTE]
  > *executeStoredProcedure* 関数を呼び出し、R 環境からストアド プロシージャを実行する場合、SQL Server 用 ODBC ドライバー 13 など、ODBC 3.8 プロバイダーを使用する必要があります。  
  
## <a name="full-reference-documentation"></a>完全なリファレンス ドキュメント

**sqlrutils** ライブラリは複数の Microsoft 製品で配布されていますが、SQL Server または別の製品のどちらから取得したライブラリでも、使用方法は同じです。 これらの関数は同じであるため、[個々の sqlrutils 関数のドキュメント](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)は Microsoft Machine Learning Server の [R リファレンス](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)の下でのみ公開されています。 製品固有の動作が存在する場合、関数のヘルプ ページにその相違点が示されます。

## <a name="functions-list"></a>関数の一覧

次のセクションでは、**sqlrutils** パッケージから呼び出すことができる関数の概要を説明します。この関数を使用すると、埋め込みの R コードを含むストアド プロシージャを作成できます。 各メソッドまたは関数のパラメーターの詳細については、パッケージの R のヘルプを参照してください。 `help(package="sqlrutils")`

|機能 | [説明] |
|------|-------------|
|[executeStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/executestoredprocedure)| SQL ストアド プロシージャを実行します。|
|[getInputParameters](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/getinputparameters)| ストアド プロシージャへの入力パラメーターの一覧を取得します。| 
|[InputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputdata)| R データ フレームで使用されるデータ ソースを SQL Server に定義します。 入力データを保存する data.frame 名、データまたは既定値を取得するクエリを指定します。 単純な SELECT クエリのみがサポートされています。 | 
|[InputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputparameter)| T-SQL スクリプトに埋め込まれる単一の入力パラメーターを定義します。 パラメーター名とその R データ型を指定する必要があります。| 
|[OutputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputdata)| R 関数で data.frame を含むリストが返される場合に必要な中間のデータ オブジェクトを生成します。 *OutputData* オブジェクトは、リストから取得された単一の data.frame の名前を格納するために使用されます。| 
|[OutputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputparameter) | R 関数でリストが返される場合に必要な中間のデータ オブジェクトを生成します。 *OutputParameter* オブジェクトは、メンバーがデータ フレームでは **ない** ことを想定し、リストの単一のメンバーの名前とデータ型を格納します。 |
|[registerStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/registerstoredprocedure) | ストアド プロシージャをデータベースに登録します。|
|[setInputDataQuery](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputdataquery)| ストアド プロシージャの入力データ パラメーターにクエリを割り当てます。| 
|[setInputParameterValue](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputparametervalue)| ストアド プロシージャの入力パラメーターに値を割り当てます。| 
|[StoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/storedprocedure)| ストアド プロシージャ オブジェクト。|


## <a name="how-to-use-sqlrutils"></a>Sqlrutils の使用方法

**sqlrutils** ライブラリ関数は、SQL Server Machine Learning (R 付属) を備えているコンピューターで実行する必要があります。クライアント ワークステーションで作業している場合は、リモートのコンピューティング コンテキストを設定して、実行を SQL Server に切り替えます。 このパッケージを使用するためのワークフローには、次の手順が含まれます。

+ ストアド プロシージャのパラメーター (入力、出力、またはその両方) の定義 
+ ストアド プロシージャの生成と登録    
+ ストアド プロシージャを実行する  

R セッションで、コマンドラインから「`library(sqlrutils)`」と入力して **sqlrutils** を読み込みます。

> [!Note]
> もしコンピューティング コンテキストを SQL Server に変更し、そのコンピューティング コンテキストでコードを実行する場合には、本ライブラリは SQL Server がないコンピューター (たとえば R クライアント インスタンス) 上で読み込むことができます。


### <a name="define-stored-procedure-parameters-and-inputs"></a>ストアド プロシージャのパラメーターと入力の定義

`StoredProcedure` はストアド プロシージャの構築に使用されるメインのコンストラクターです。 このコンストラクターは、 *SQL Server ストアド プロシージャ* オブジェクトを生成し、オプションで T-SQL コマンドを使用したストアド プロシージャの生成に使用できるクエリを含むテキスト ファイルを作成します。 

*StoredProcedure* 関数では、オプションで、指定したインスタンスとデータベースを使用してストアド プロシージャを登録することもできます。

+ 有効な R 関数を指定するには、 `func` 引数を使用します。 この関数が使用するすべての変数は、関数内に定義するか、入力パラメーターとして渡される必要があります。 これらのパラメーターには、最大でデータ フレームを 1 つ含めることが可能です。

+ R 関数は、データ フレーム、名前付きのリスト、NULL 値のいずれかを返す必要があります。 関数がリストを返す場合、リストには最大で 1 つの data.frame のみ含めることができます。

+ 作成するストアド プロシージャの名前を指定するには、 `spName` 引数を使用します。

+ `setInputData`、 `setInputParameter`および `setOutputParameter`のヘルパー関数によって作成されるオブジェクトを使用することにより、オプションの入力および出力パラメーターに渡すことができます。

+  作成する .sql ファイルに名前とパスを提供する場合、オプションで `filePath` を使用します。 このファイルを SQL Server インスタンスで実行すると、T-SQL を使用したストアド プロシージャを生成できます。

+ ストアド プロシージャの保存先のサーバーおよびデータベースを定義するには、 `dbName` と  `connectionString`の引数を使用します。

+ 特定の *StoredProcedure* オブジェクトを作成するのに使用された *InputData* と *InputParameter* オブジェクトのリストを取得するには、 `getInputParameters`を呼び出します。 

+ 指定したデータベースにストアド プロシージャを登録するには、 `registerStoredProcedure`を使用します。

ストアド プロシージャ オブジェクトには、既定値が指定されている場合を除き、通常データや値は関連付けられていません。 ストアド プロシージャが実行されるまで、データは取得されません。 

### <a name="specify-inputs-and-execute"></a>入力を指定して実行する

+ `setInputDataQuery` を使用して、 *InputParameter* オブジェクトにクエリを割り当てます。 たとえば、R でストアド プロシージャ オブジェクトを作成した場合、必要な入力を使用してストアド プロシージャを実行するには、 `setInputDataQuery` を使用して *StoredProcedure* 関数に引数を渡します。

+ `setInputValue` InputParameter *オブジェクトとして格納されているパラメーターに特定の値を割り当てるには、* を使用します。 次に、 *StoredProcedure* 関数にパラメーター オブジェクトとその値の割り当てを渡し、ストアド プロシージャを設定値で実行します。

+ `executeStoredProcedure` StoredProcedure *オブジェクトとして定義されたストアド プロシージャを実行するには、* を使用します。 この関数は、R コードからこのストアド プロシージャを実行する場合のみ呼び出します。 T-SQL を使用して SQL Server からストアド プロシージャを実行する場合は使用しないでください。

> [!NOTE]
> *executeStoredProcedure* 関数には、SQL Server 用の ODBC ドライバー 13 などの ODBC 3.8 プロバイダーが必要です。  

## <a name="see-also"></a>参照

[sqlrutils を使用してストアド プロシージャを作成する方法](how-to-create-a-stored-procedure-using-sqlrutils.md)

