---
title: Python 言語拡張機能
description: SQL Server Machine Learning Services での Python コードの実行と組み込み Python ライブラリについて学習します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0445fb83a1ee4c4e2a991df8e698f24988454d19
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727675"
---
# <a name="python-language-extension-in-sql-server"></a>SQL Server の Python 言語拡張機能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Python 拡張機能は、リレーショナル データベース エンジンに対する SQL Server Machine Learning Services アドオンの一部です。 これによって追加されるのは、Python の実行環境、Python 3.5 ランタイムとインタープリターを含む Anaconda ディストリビューション、標準ライブラリとツール、および Python 用の Microsoft 製品ライブラリ (大規模な分析用の [revoscalepy](../python/ref-py-revoscalepy.md) と機械学習アルゴリズム用の [microsoftml](../python/ref-py-microsoftml.md)) です。 

Python 統合は [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) としてインストールされます。

Python 3.5 ランタイムとインタープリターのインストールにより、標準的な Python ソリューションとのほぼ完全な互換性が確保されます。 Python は SQL Server とは別のプロセスで実行されるので、データベース操作に支障はありません。

## <a name="python-components"></a>Python コンポーネント

SQL Server には、オープンソース パッケージと専用パッケージの両方が含まれています。 セットアップによってインストールされる Python ランタイムは、Python 3.5 を含む Anaconda 4.2 です。 Python ランタイムは、SQL ツールとは別にインストールされ、機能拡張フレームワークのコア エンジン プロセスの外部で実行されます。 Machine Learning Services と Python のインストールの一環として、GNU Public License の条項に同意する必要があります。 

SQL Server では、Python 実行可能ファイルは変更されませんが、セットアップによってインストールされたバージョンの Python を使用する必要があります。これは、専用パッケージがビルドおよびテストされているバージョンであるためです。 Anaconda ディストリビューションでサポートされているパッケージの一覧については、Continuum 分析サイト「[Anaconda package list](https://docs.continuum.io/anaconda/packages/pkg-docs)」(Anaconda パッケージ リスト) を参照してください。

特定のデータベース エンジン インスタンスに関連付けられている Anaconda ディストリビューションは、そのインスタンスに関連付けられているフォルダーで見つけることができます。 たとえば、SQL Server 2017 データベース エンジンと共に Machine Learning Services および Python を既定のインスタンスにインストールした場合は、`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES` を確認します。

Microsoft が並列ワークロードと分散ワークロード用に追加した Python パッケージには、次のライブラリが含まれます。

| ライブラリ | [説明] |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | データ ソース オブジェクトとデータの探索、操作、変換、視覚化をサポートします。 リモート コンピューティング コンテキスト、およびさまざまなスケーラブルな機械学習モデル (**rxLinMod** など) の作成をサポートします。 詳細については、[SQL Server での revoscalepy モジュール](../python/ref-py-revoscalepy.md)に関するページをご覧ください。  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 速度と精度のために最適化された機械学習アルゴリズムに加え、テキストとイメージを操作するためのインライン変換も含まれています。 詳細については、[SQL Server での microsoftml モジュール](../python/ref-py-microsoftml.md)に関するページを参照してください。 |

microsoftml と revoscalepy は密結合されています。microsoftml で使用されるデータ ソースは、revoscalepy オブジェクトとして定義されています。 revoscalepy でコンピューティング コンテキストの制限は microsoftml に転送されます。 つまり、ローカル操作ではすべての機能を使用できますが、リモート コンピューティング コンテキストに切り替えるには RxInSqlServer が必要です。

## <a name="using-python-in-sql-server"></a>SQL Server での Python の使用

ご利用の Python コードに **revoscalepy** モジュールをインポートしてから、他の Python 関数と同様に、モジュールから関数を呼び出します。

サポートされているデータ ソースには、ODBC データベース、SQL Server、他のソースまたは R ソリューションとデータを交換するための XDF ファイル形式があります。 Python に対する入力データは表形式とする必要があります。 Python の結果はすべて、**Pandas** データ フレームの形式で返される必要があります。

サポートされているコンピューティング コンテキストには、ローカルまたはリモートの SQL Server コンピューティング コンテキストが含まれます。 リモート コンピューティング コンテキストとは、ワークステーションなどの 1 台のコンピューターで起動するコード実行を指しますが、その後、スクリプトの実行はリモート コンピューターに切り替えられます。 コンピューティング コンテキストを切り替えるには、両方のシステムに同じ revoscalepy ライブラリが用意されている必要があります。

ご想像のとおり、ローカルのコンピューティング コンテキストには、データベース エンジン インスタンスと同じサーバー上での Python コードの実行に加え、T-SQL 内のコードまたはストアド プロシージャに埋め込まれたコードの実行も含まれます。 また、リモートのコンピューティング コンテキストを定義することにより、ローカルの Python IDE からコードを実行し、SQL Server コンピューター上でスクリプトを実行することもできます。

## <a name="execution-architecture"></a>アーキテクチャの実行

以下の図は、サポートされている各シナリオでの SQL Server コンポーネントと Python ランタイムとのやりとりを示しています。そのシナリオとは、SQL Server コンピューティング コンテキストを使用したデータベース内のスクリプトの実行と Python ターミナルからのリモート実行です。

### <a name="python-scripts-executed-in-database"></a>データベース内で実行される Python スクリプト

SQL Server の "内部で" Python を実行する場合は、Python スクリプトを特殊なストアド プロシージャである [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) にカプセル化する必要があります。

ストアド プロシージャにスクリプトが埋め込まれたら、ストアド プロシージャを呼び出すことができる任意のアプリケーションで、Python コードの実行を開始できます。  その後は、SQL Server により、次の図にまとめたように、コードの実行が管理されます。

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. ストアド プロシージャに渡されたパラメーター `@language='Python'` によって、Python ランタイムに対する要求が示されます。 この要求は SQL Server からスタート パッド サービスに送信されます。
Linux の場合、SQL では**スタート パッド** サービスを使用して、ユーザーごとに個別のスタート パッド プロセスとの通信が行われます。 詳細については、[機能拡張アーキテクチャの図](extensibility-framework.md#architecture-diagram)を参照してください。
2. スタート パッド サービスによって適切なランチャーが起動されます (この場合は PythonLauncher)。
3. PythonLauncher によって外部の Python35 プロセスが開始されます。
4. BxlServer と Python ランタイムとの連携により、データ交換や、作業結果の保存が管理されます。
5. SQL サテライトでは、関連するタスクやプロセスについての SQL Server との通信が管理されます。
6. BxlServer では、SQL サテライトを使用して、状態と結果が SQL Server に通知されます。
7. SQL Server では、結果が取得され、関連するタスクとプロセスが終了されます。

### <a name="python-scripts-executed-from-a-remote-client"></a>リモート クライアントから実行される Python スクリプト

次の条件が満たされている場合は、ラップトップなどのリモート コンピューターから Python スクリプトを実行し、SQl Server コンピューターのコンテキストでそれらを実行することができます。

+ スクリプトが適切に設計されています。
+ リモート コンピューターには、Machine Learning Services で使用される機能拡張ライブラリがインストールされています。 リモート コンピューティング コンテキストを使用するには、[revoscalepy](../python/ref-py-revoscalepy.md) パッケージが必要です。

次の図は、リモート コンピューターからスクリプトが送信される場合の全体的なワークフローをまとめたものです。

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. **revoscalepy** でサポートされている関数の場合、Python ランタイムによってリンク関数が呼び出され、続いてこの関数によって BxlServer が呼び出されます。
2. BxlServer は Machine Learning Services (データベース内) に含まれており、Python ランタイムとは別のプロセスで実行されます。
3. BxlServer では接続のターゲットが決定され、ODBC を使用して接続が開始され、Python スクリプト内の接続文字列の一部として提供された資格情報が渡されます。
4. BxlServer によって、SQL Server インスタンスへの接続が開かれます。
5. 外部スクリプト ランタイムが呼び出されると、スタート パッド サービスが呼び出され、続いて適切なランチャー (この場合は、PythonLauncher.dll) が起動されます。 その後、Python コードの処理は、T-SQL のストアド プロシージャから Python コードが呼び出される場合と同様のワークフローで処理されます。
6. PythonLauncher では、SQL Server コンピューターにインストールされている Python のインスタンスへの呼び出しが行われます。
7. 結果が BxlServer に返されます。
8. SQL サテライトでは、SQL Server との通信と、関連するジョブ オブジェクトのクリーンアップが管理されます。
9. SQL Server からクライアントに結果が返されます。

## <a name="next-steps"></a>次の手順

+ [SQL Server の revoscalepy モジュール](../python/ref-py-revoscalepy.md)
+ [revoscalepy 関数リファレンス](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [SQL Server の機能拡張フレームワーク](extensibility-framework.md)
+ [SQL Server の R および機械学習拡張機能](extension-r.md)
+ [Python パッケージ情報の取得](../package-management/python-package-information.md)
+ [sqlmlutils を使用して Python パッケージをインストールする](../package-management/install-additional-python-packages-on-sql-server.md)
