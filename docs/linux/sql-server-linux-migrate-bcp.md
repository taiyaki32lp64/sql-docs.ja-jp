---
title: データを SQL Server on Linux に一括コピーする
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: b611ef63532dd855648354bb85fc96f7cb52bd60
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68127321"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>bcp を使用してデータを SQL Server on Linux に一括コピーする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、[bcp](../tools/bcp-utility.md) コマンドライン ユーティリティを使用して、ユーザーが指定した形式で SQL Server on Linux のインスタンスとデータ ファイルとの間でデータを一括コピーする方法について説明します。

`bcp` を使用すると、大量の行を SQL Server テーブルにインポートすることや、SQL Server テーブルからデータ ファイルにデータをエクスポートすることができます。 queryout オプションと併用する場合を除き、`bcp` では Transact-SQL の知識は必要ありません。 `bcp` コマンドライン ユーティリティは、オンプレミスまたはクラウドの Linux、Windows、または Docker で実行されている Microsoft SQL Server、および Azure SQL Database または Azure SQL Data Warehouse で使用できます。

この記事で取り上げるテクニック:
- `bcp in` コマンドを使用してテーブルにデータをインポートする
- `bcp out` コマンドを使用してテーブルからデータをエクスポートする

## <a name="install-the-sql-server-command-line-tools"></a>SQL Server コマンドライン ツールをインストールする

`bcp` は SQL Server のコマンドライン ツールの一部です。これらは、SQL Server on Linux と共に自動的にインストールされません。 Linux マシンに SQL Server コマンドライン ツールをまだインストールしていない場合は、インストールする必要があります。 ツールをインストールする方法の詳細については、次の一覧から Linux ディストリビューションを選択してください。

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>bcp を使用してデータをインポートする

このチュートリアルでは、ローカル SQL Server インスタンス (**localhost**) にサンプル データベースとテーブルを作成し、`bcp` を使用してディスク上のテキスト ファイルからサンプル テーブルに読み込みます。

### <a name="create-a-sample-database-and-table"></a>サンプル データベースとテーブルを作成する

まず、このチュートリアルの残りの部分で使用する単純なテーブルを含むサンプル データベースを作成します。

1. Linux ボックスで、コマンド ターミナルを開きます。

2. 次のコマンドをコピーしてターミナル ウィンドウに貼り付けます。 これらのコマンドは、**sqlcmd** コマンドライン ユーティリティを使用して、サンプル データベース (**BcpSampleDB**) とテーブル (**TestEmployees**) をローカル SQL Server インスタンス (**localhost**) に作成します。 コマンドを実行する前に、必要に応じて `username` と`<your_password>` を置き換えます。

データベース **BcpSampleDB** を作成します。
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
データベース **BcpSampleDB** にテーブル **TestEmployees** を作成します。
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>ソース データ ファイルを作成する
次のコマンドをコピーしてターミナル ウィンドウに貼り付けます。 組み込みの `cat` コマンドを使用して、3 つのレコードがあるサンプル テキスト データ ファイルを作成し、ホーム ディレクトリに **~/test_data.txt** という名前でファイルを保存します。 レコード内のフィールドはコンマ区切りです。

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

ターミナル ウィンドウで次のコマンドを実行して、データ ファイルが正しく作成されたことを確認できます。
```bash 
cat ~/test_data.txt
```

これにより、ターミナル ウィンドウに次の内容が表示されます。
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>ソース データ ファイルからデータをインポートする
次のコマンドをコピーしてターミナル ウィンドウに貼り付けます。 このコマンドでは、`bcp` を使用してローカルの SQL Server インスタンス (**localhost**) に接続し、データ ファイル ( **~/test_data.txt**) のデータをデータベース (**BcpSampleDB**) のテーブル (**TestEmployees**) にインポートします。 コマンドを実行する前に、必要に応じてユーザー名と `<your_password>` を置き換えます。

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

この例で `bcp` に使用したコマンドライン パラメーターの概要は次のとおりです。
- `-S`: 接続先となる SQL Server のインスタンスを指定します
- `-U`: SQL Server への接続に使用されるログイン ID を指定します
- `-P`: ログイン ID のパスワードを指定します
- `-d`: 接続先のデータベースを指定します
- `-c`: 文字データ型を使用して操作を実行します
- `-t`: フィールド ターミネータを指定します。 ここでは、データ ファイル内のレコードのフィールド ターミネータとして `comma` を使用しています

> [!NOTE]
> この例では、カスタムの行ターミネータを指定していません。 以前に `cat` コマンドを使用してデータ ファイルを作成したときは、テキスト データ ファイルの行は `newline` で正しく終了していました。

ターミナル ウィンドウで次のコマンドを実行して、データが正常にインポートされたことを確認できます。 コマンドを実行する前に、必要に応じて `username` と `<your_password>` を置き換えます。
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

これにより、次の結果が表示されます。
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>bcp を使用してデータをエクスポートする

このチュートリアルでは、`bcp` を使用して、先ほど作成したサンプル テーブルのデータを新しいデータ ファイルにエクスポートします。

次のコマンドをコピーしてターミナル ウィンドウに貼り付けます。 これらのコマンドでは、`bcp` コマンドライン ユーティリティを使用し、データベース **BcpSampleDB** のテーブル **TestEmployees** から **~/test_export.txt** という新しいデータ ファイルにデータをエクスポートします。  コマンドを実行する前に、必要に応じてユーザー名と `<your_password>` を置き換えます。

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

ターミナル ウィンドウで次のコマンドを実行して、データが正しくエクスポートされたことを確認できます。
```bash 
cat ~/test_export.txt
```

これにより、ターミナル ウィンドウに次の内容が表示されます。
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>参照
- [bcp ユーティリティ](../tools/bcp-utility.md)
- [bcp を使用した互換性のためのデータ形式の指定](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [BULK INSERT を使用した一括データのインポート](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
