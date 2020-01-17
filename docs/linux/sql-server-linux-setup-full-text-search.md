---
title: Linux に SQL Server フルテキスト検索をインストールする
description: この記事では、Linux に SQL Server フルテキスト検索をインストールする方法について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.openlocfilehash: 2f99310a1eaa240db15b4db5f686a4d6cc49c186
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874764"
---
# <a name="install-sql-server-full-text-search-on-linux"></a>Linux に SQL Server フルテキスト検索をインストールする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

以下の手順では、Linux に [SQL Server フルテキスト検索](../relational-databases/search/full-text-search.md) (**mssql-server-fts**) をインストールします。 フルテキスト検索を使うと、SQL Server テーブル内の文字ベースのデータに対してフルテキスト クエリを実行できます。 このリリースの既知の問題については、[リリース ノート](sql-server-linux-release-notes.md)をご覧ください。

> [!NOTE]
> SQL Server フルテキスト検索をインストールする前に、まず [SQL Server をインストール](sql-server-linux-setup.md#platforms)してください。 これにより、**mssql-server-fts** パッケージをインストールするときに使うキーとリポジトリが構成されます。

ご自身のプラットフォームに合わせて SQL Server フルテキスト検索をインストールします。

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">RHEL へのインストール</a>

次のコマンドを使って、Red Hat Enterprise Linux に **mssql-server-fts** をインストールします。 

```bash
sudo yum install -y mssql-server-fts
```

既に **mssql-server-fts** をインストールしている場合は、次のコマンドを使って最新バージョンに更新できます。

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

オフライン インストールが必要な場合は、[リリース ノート](sql-server-linux-release-notes.md)に記載されているフルテキスト検索のパッケージのダウンロードを探します。 次に、[SQL Server のインストール](sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

## <a name="ubuntu">Ubuntu へのインストール</a>

次のコマンドを使って、Ubuntu に **mssql-server-fts** をインストールします。 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

既に **mssql-server-fts** をインストールしている場合は、次のコマンドを使って最新バージョンに更新できます。

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

オフライン インストールが必要な場合は、[リリース ノート](sql-server-linux-release-notes.md)に記載されているフルテキスト検索のパッケージのダウンロードを探します。 次に、[SQL Server のインストール](sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

## <a name="SLES">SLES へのインストール</a>

次のコマンドを使って、SUSE Linux Enterprise Server に **mssql-server-fts** をインストールします。 

```bash
sudo zypper install mssql-server-fts
```

既に **mssql-server-fts** をインストールしている場合は、次のコマンドを使って最新バージョンに更新できます。

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

オフライン インストールが必要な場合は、[リリース ノート](sql-server-linux-release-notes.md)に記載されているフルテキスト検索のパッケージのダウンロードを探します。 次に、[SQL Server のインストール](sql-server-linux-setup.md#offline)の記事で説明されているのと同じオフライン インストール手順を使用します。

## <a name="supported-languages"></a>サポートされている言語

フルテキスト検索では、言語に基づいて個々の単語の識別方法を決定する、[ワード ブレーカー](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)が使われています。 **sys.fulltext_languages** カタログ ビューに対してクエリを実行することで、登録されているワード ブレーカーの一覧を取得できます。 以下の言語のワード ブレーカーが SQL Server と共にインストールされます。

| [言語] | 言語 ID |
|---|---|
| ニュートラル | 0 |
| アラビア語 | 1025 |
| ベンガル語 (インド) | 1093 |
| ブークモール | 1044 |
| ポルトガル語 (ブラジル) | 1046 |
| 英語 (U.K.) | 2057 |
| Bulgarian | 1026 |
| カタロニア語 | 1027 |
| 中国語 (中華人民共和国香港特別行政区) | 3076 |
| 中国語 (中華人民共和国マカオ特別行政区) | 5124 |
| 中国語 (シンガポール) | 4100 |
| Croatian | 1050 |
| Czech | 1029 |
| Danish | 1030 |
| Dutch | 1043 |
| English | 1033 |
| French | 1036 |
| German | 1031 |
| Greek | 1032 |
| グジャラート語 | 1095 |
| ヘブライ語 | 1037 |
| ヒンディー語 | 1081 |
| アイスランド語 | 1039 |
| インドネシア語 | 1057 |
| Italian | 1040 |
| Japanese | 1041 |
| カンナダ語 | 1099 |
| Korean | 1042 |
| Latvian | 1062 |
| Lithuanian | 1063 |
| マレー語 - マレーシア | 1086 |
| マラヤーラム語 | 1100 |
| マラーティー語 | 1102 |
| Polish | 1045 |
| Portuguese | 2070 |
| パンジャーブ語 | 1094 |
| Romanian | 1048 |
| Russian | 1049 |
| セルビア語 (キリル) | 3098 |
| セルビア語 (ラテン) | 2074 |
| Simplified Chinese | 2052 |
| Slovak | 1051 |
| Slovenian | 1060 |
| Spanish | 3082 |
| Swedish | 1053 |
| タミール語 | 1097 |
| テルグ語 | 1098 |
| Thai | 1054 |
| Traditional Chinese | 1028 |
| Turkish | 1055 |
| ウクライナ語 | 1058 |
| ウルドゥ語 | 1056 |
| ベトナム語 | 1066 |

## <a id="filters"></a> フィルター

フルテキスト検索では、バイナリ ファイルに格納されているテキストも操作できます。 ただし、この場合は、ファイルを処理するためにインストール済みのフィルターが必要です。 フィルターの詳細については、「[検索用フィルターの構成と管理](../relational-databases/search/configure-and-manage-filters-for-search.md)」をご覧ください。

インストールされているフィルターの一覧を確認するには、**sp_help_fulltext_system_components 'filter'** を呼び出します。 SQL Server には、以下のフィルターがインストールされています。

| [コンポーネント名] | クラス ID | Version |
|---|---|---|
|.a | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ans | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.asc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ascx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asm | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.asp | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.aspx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asx | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bas | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bat | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.bcp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.c | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cls | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cmd | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.csa | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.css | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.csv | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dbs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.def | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dic | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dos | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.dsp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.dsw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ext | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.faq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.fky | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.h | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hhc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hta | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.html | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htt | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htw | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.i | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ibq | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ics | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.idl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.idq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.inc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ini | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.inx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.jav | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.java | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.js | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.kci | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.lgn | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.log | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.m3u | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.mak | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.mk | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.odh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgdef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgundef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.prc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rc2 | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.reg | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rgs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rtf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rul | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.s | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.scc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.shtm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.shtml | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.snippet | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sol | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sor | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.srf | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.stm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.tab | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tdl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tlh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tli | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.trg | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.txt | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.udf | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.udt | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.url | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.usr | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vbs | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.viw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixlangpack | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixmanifest | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vspscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vssscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wri | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wtx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.xml | 41B9BE05-B3AF-460C-BF0B-2CDD44A093B1 | 12.0.9735.0 |

## <a name="semantic-search"></a>セマンティック検索
フルテキスト検索の機能に基づく[セマンティック検索](../relational-databases/search/semantic-search-sql-server.md)では、統計的に関連性がある*キー フレーズ*を抽出してインデックスを作成します。 これにより、データベースのドキュメント内の意味に対してクエリを実行できるようになります。 また、これは類似したドキュメントを識別するのにも役立ちます。

セマンティック検索を使用するためには、まず使用するコンピューターにセマンティック言語統計データベースを復元する必要があります。

1. [sqlcmd](sql-server-linux-setup-tools.md) などのツールを使い、Linux の SQL Server インスタンス上で次の Transact-SQL コマンドを実行します。 このコマンドによって、言語統計データベースが復元されます。

   ```sql
   RESTORE DATABASE [semanticsdb] FROM
   DISK = N'/opt/mssql/misc/semanticsdb.bak' WITH FILE = 1,
   MOVE N'semanticsdb' TO N'/var/opt/mssql/data/semanticsDB.mdf',
   MOVE N'semanticsdb_log' TO N'/var/opt/mssql/data/semanticsdb_log.ldf', NOUNLOAD, STATS = 5
   GO
   ```

   > [!NOTE]
   > 必要に応じて、使用する構成に合うように前の RESTORE コマンドに含まれているパスを更新してください。

1. 次の Transact-SQL コマンドを実行して、セマンティック言語統計データベースを登録します。

    ```sql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO
    ```

## <a name="next-steps"></a>次の手順

フルテキスト検索の詳細については、[SQL Server フルテキスト検索](../relational-databases/search/full-text-search.md)に関する記事をご覧ください。 
