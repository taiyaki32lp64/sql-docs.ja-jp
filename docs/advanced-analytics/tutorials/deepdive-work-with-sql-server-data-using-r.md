---
title: RevoScaleR チュートリアルのデータベース
description: R チュートリアル用の SQL Server データベースを作成する方法について詳しく説明しているチュートリアルです。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 537bfb64562dfad9dbefbce70423892cd6e1e431
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727125"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>データベースとアクセス許可を作成する (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

レッスン 1 では、SQL Server データベースの設定と、このチュートリアルを完了するために必要なアクセス許可について説明します。 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) または別のクエリ エディターを使用して、次のタスクを完了します。

> [!div class="checklist"]
> * 2 つの R モデルのトレーニングとスコアリングに使用するデータを格納するための新しいデータベースを作成します
> * データベース オブジェクトを作成および使用するための権限を持つデータベース ユーザー ログインを作成する
  
## <a name="create-the-database"></a>データベースの作成

このチュートリアルでは、データとコードを格納するデータベースが必要です。 管理者でない場合は、DBA に、データベースとあなたのログイン情報の作成を依頼してください。 データの書き込みと読み取り、および R スクリプトの実行をするためのアクセス許可が必要です。

1. SQL Server Management Studio で、R が有効にされたデータベース インスタンスに接続します。

2. **[データベース]** を右クリックして、 **[新しいデータベース]** をクリックします。
  
2. 新しいデータベースの名前を入力します:RevoDeepDive。
  

## <a name="create-a-login"></a>ログインを作成します
  
1. **[新しいクエリ]** をクリックして、データベース コンテキストを master データベースに変更します。
  
2. 新しい **[クエリ]** ウィンドウで、次のコマンドを実行してユーザー アカウントを作成し、このチュートリアルで使用するデータベースに割り当てます。 必要に応じてデータベースの名前を変更します。

3. ログインを確認するには、新しいデータベースを選択し、 **[セキュリティ]** 、 **[ユーザー]** の順に展開します。
  
**Windows ユーザー**
  
```sql
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[RevoDeepDive]

 --Add the new user to tutorial database
USE [RevoDeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**SQL ログイン**

```sql
-- Create new SQL login
USE master
GO
CREATE LOGIN [DDUser01] WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE RevoDeepDive
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

## <a name="assign-permissions"></a>アクセス許可の割り当て

このチュートリアルでは、R スクリプトと DDL 操作のデモを実行します。これには、テーブルとストアド プロシージャの作成と削除、および SQL Server における外部プロセスの R スクリプトの実行が含まれます。 この手順では、これらのタスクを許可するためのアクセス許可を割り当てます。

この例では、SQL ログイン (DDUser01) が想定されていますが、Windows ログインを作成した場合は、それを代わりに使用します。

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>接続のトラブルシューティング

このセクションでは、データベースを設定する過程で発生する可能性がある一般的な問題を示します。

- **データベースの接続と SQL クエリを確認するにはどうすればよいですか。**
  
    サーバーを使用して R コードを実行する前に、R の開発環境からデータベースにアクセスできることを確認したい場合があります。 [Visual Studio のサーバー エクスプローラー](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) と [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) はどちらも、強力なデータベース接続と管理機能を持つ無償のツールです。
  
    新しいデータベース管理ツールをインストールしたくない場合は、コントロール パネルの [ODBC データ ソース アドミニストレーター](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) を使用して、SQL Server インスタンスへのテスト接続を作成できます。 データベースが正しく構成されていて、正しいユーザー名とパスワードを入力した場合は、先に作成したデータベースを表示し、既定のデータベースとして選択することができます。
  
    接続エラーの一般的な理由として、サーバーに対してリモート接続が有効になっていない、および名前付きパイプ プロトコルが有効になっていないことが挙げられます。 この記事では、その他のトラブルシューティングのヒントを得ることができます。[SQL Server データベース エンジンへの接続のトラブルシューティング](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine)。
  
- **テーブル名に datareader というプレフィックスが付くのはなぜですか。**
  
    このユーザーの既定のスキーマを **db_datareader** と指定すると、このユーザーが作成したすべてのテーブルとその他の新しいオブジェクトの名前の前に、この*スキーマ*名が付加されます。 スキーマは、オブジェクトを整理するためにデータベースに追加できるフォルダーのようなものです。 スキーマでは、データベース内でのユーザーの権限も定義されています。
  
    スキーマが 1 つの特定のユーザー名に関連付けられている場合は、そのユーザーが_スキーマの所有者_です。 オブジェクトを作成するときは、別のスキーマに作成することを明示的に要求しない限り、常に自分用のスキーマに作成されます。
  
    たとえば、**TestData** という名前のテーブルを作成し、既定のスキーマが **db_datareader** である場合、テーブルは `<database_name>.db_datareader.TestData` という名前で作成されます。
  
    このため、テーブルが異なるスキーマに属していれば、1 つのデータベースに同じ名前の複数のテーブルを含めることができます。
   
    テーブルを検索するときにスキーマを指定しないと、データベース サーバーはユーザーが所有するスキーマを探します。 そのため、自分のログインに関連付けられているスキーマ内のテーブルにアクセスするときは、スキーマ名を指定する必要はありません。
  
- **DDL 特権を持っていません。それでもチュートリアルを実行できますか。**
  
    はい。ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにデータを事前に読み込んで、次のレッスンに進むように依頼する必要があります。 DDL 特権が必要な関数は、可能なときにはいつでもチュートリアルで呼び出されます。

    また、管理者に、すべての外部スクリプトを実行する権限を付与してくれるよう依頼します。 これは、リモートまたは `sp_execute_external_script` を使用して R スクリプトを実行する場合に必要です。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [RxSqlServerData を使用して SQL Server のデータ オブジェクトを作成する](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)