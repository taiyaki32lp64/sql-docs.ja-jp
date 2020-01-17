---
title: R スクリプトのトラブルシューティング
description: この記事では、SQL Server で R コードを実行する際のいくつかのスクリプト エラーについて説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d1cfd06fd881c4749879365feda14e3cfcb877a9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727503"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server での R スクリプト エラー
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server で R コードを実行する際のいくつかのスクリプト エラーについて説明します。 この一覧がすべてではありません。 パッケージは多数あり、同じパッケージのバージョンによってエラーが異なる場合があります。 スクリプト エラーは [Machine Learning Server フォーラム](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)に投稿することをお勧めします。ここでは、R Services (データベース内)、Microsoft R Client、Microsoft R Server で使用される機械学習コンポーネントへの支援が提供されています。

## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>T-SQL またはストアド プロシージャで有効なスクリプトが失敗する

ストアド プロシージャに R コードをラップする前に、外部 IDE や、RTerm または Rterm などのいずれかの R ツールで R コードを実行することをお勧めします。 これらの方法を使用することで、R によって返される詳細なエラー メッセージを使用して、コードをテストおよびデバッグできます。

ただし、外部 IDE やユーティリティで完全に動作するコードが、ストアド プロシージャや SQL Server の計算コンテキストでは実行に失敗することがあります。 この問題が発生した場合は、そのパッケージが SQL Server で動作しないと判断する前に、確認すべきさまざまな問題があります。

1. Launchpad が実行されているかどうかを確認します。

2. メッセージを調べて、入力データまたは出力データに互換性のないデータ型またはサポートされていないデータ型の列が含まれているかどうかを確認します。 たとえば、SQL データベースに対するクエリでは、GUID または RowGUID が返されることがよくありますが、これらはどちらもサポートされていません。 詳しくは、[R のライブラリとデータ型](r/r-libraries-and-data-types.md)に関する記事をご覧ください。

3. 個々の R 関数のヘルプ ページを参照して、SQL Server 計算コンテキストですべてのパラメーターがサポートされているかどうかを確認します。 ScaleR のヘルプについては、インライン R ヘルプ コマンドを使用するか、[パッケージ リファレンス](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)を参照してください。

R ランタイムが機能していても、スクリプトからエラーが返された場合は、R Tools for Visual Studio などの専用の R 開発環境でスクリプトをデバッグしてみることをお勧めします。

また、R とデータベース エンジンの間でデータを移動するときに発生する可能性のあるデータ型に関する問題を修正するために、スクリプトを確認し、少し書き直すことをお勧めします。 詳しくは、[R のライブラリとデータ型](r/r-libraries-and-data-types.md)に関する記事をご覧ください。

また、sqlrutils パッケージを使用して、ストアド プロシージャとしてより簡単に使用できる形式で R スクリプトをバンドルすることもできます。 詳細については、以下をご覧ください。
* [sqlrutils パッケージ](r/ref-r-sqlrutils.md)
* [sqlrutils を使用してストアド プロシージャを作成する](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>スクリプトが一貫性のない結果を返す

R スクリプトは次のいくつかの理由により、SQL Server のコンテキストで異なる値を返すことがあります。

- データが SQL Server と R の間で渡されるときに、一部のデータ型で暗黙的な型変換が自動的に実行されます。詳細については、[R のライブラリとデータ型](r/r-libraries-and-data-types.md)に関する記事を参照してください。

- ビットが要因であるかどうかを判別します。 たとえば、32 ビットと 64 ビットの浮動小数点ライブラリでは、算術演算の結果に違いがあることがよくあります。

- 演算中に NAN が生成されたかどうかを判別します。 これにより、結果が無効になることがあります。

- ゼロに近い数値の逆数を取ると、小さい違いが増幅される可能性があります。

- 丸め誤差が累積すると、0 ではなく 0 未満の値が発生する可能性があります。

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>ODBC 経由のリモート実行に対する暗黙の認証

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンピューターに接続し、**RevoScaleR** 関数を使用して R コマンドを実行した場合、データをサーバーに書き込む ODBC 呼び出しを使用するときにエラーが発生することがあります。 このエラーは、Windows 認証を使用している場合にのみ発生します。

その理由は、R Services に対して作成されるワーカー アカウントに、サーバーに接続するためのアクセス許可がないためです。 そのため、ODBC 呼び出しをユーザーに代わって実行することはできません。 この問題は SQL ログインでは発生しません。SQL ログインでは、資格情報が R クライアントから SQL Server インスタンスに明示的に渡され、次に ODBC に渡されるためです。 ただし、SQL ログインを使用すると、Windows 認証を使用した場合よりも安全性が低くなります。

リモートで開始されるスクリプトから Windows 資格情報を安全に渡すには、SQL Server が資格情報をエミュレートする必要があります。 このプロセスは _暗黙の認証_と呼ばれます。 これを機能させるには、SQL Server コンピューターで R スクリプトまたは Python スクリプトを実行するワーカー アカウントに適切なアクセス許可が必要です。

1. R コードを実行するインスタンスで管理者として [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開きます。

2. 次のスクリプトを実行します。 ユーザー グループの名前 (既定値を変更した場合) と、コンピューターとインスタンスの名前を必ず編集してください。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>SQL 計算コンテキストで R を実行しているときにワークスペースをクリアしないようにする

R コンソールでの操作時にワークスペースをクリアすることはよくありますが、SQL 計算コンテキストで意図しない結果になる場合があります。

`revoScriptConnection` は、SQL Server から呼び出される R セッションに関する情報を含む R ワークスペース内のオブジェクトです。 ただし、R コードにワークスペースをクリアするためのコマンド (`rm(list=ls())`など) が含まれている場合は、R ワークスペース内のセッションおよび他のオブジェクトに関するすべての情報もクリアされます。

回避策としては、SQL Server で R を実行しているときは、変数や他のオブジェクトを無差別にクリアしないようにします。 特定の変数を削除するには、**remove** 関数を使用します。

```R
remove('name1', 'name2', ...)
```

削除する変数が複数ある場合は、リストに一時変数の名前を保存し、そのリストでガベージ コレクションを定期的に実行することをお勧めします。



## <a name="next-steps"></a>次の手順

[Machine Learning Services のトラブルシューティングと既知の問題](machine-learning-troubleshooting-faq.md)

[機械学習のトラブルシューティングのためのデータ収集](data-collection-ml-troubleshooting-process.md)

[アップグレードとインストールに関してよく寄せられる質問](r/upgrade-and-installation-faq-sql-server-r-services.md)

[データベース エンジンの接続のトラブルシューティング](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
