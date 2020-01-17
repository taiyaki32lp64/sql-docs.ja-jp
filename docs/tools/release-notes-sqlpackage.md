---
title: DacFx と SqlPackage のリリース ノート | Microsoft Docs
description: Microsoft sqlpackage のリリース ノート。
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: 11e10f4a29b15efbd2b0ee513080a2000ae7e2f1
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73033051"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe のリリース ノート

**[最新バージョンのダウンロード](sqlpackage-download.md)**

この記事では、SqlPackage.exe のリリースされたバージョンによって提供される機能と修正プログラムを示します。

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="184-sqlpackage"></a>18.4 sqlpackage

|プラットフォーム|ダウンロード|リリース日|Version|ビルド
|:---|:---|:---|:---|:---|
|Windows|[MSI インストーラー](https://go.microsoft.com/fwlink/?linkid=2108813)|2019 年 10 月 29 日|18.4|15.0.4573.2|
|macOS .NET Core |[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2108815)|2019 年 10 月 29 日| 18.4|15.0.4573.2|
|Linux .NET Core |[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2108814)|2019 年 10 月 29 日| 18.4|15.0.4573.2|
|Windows .NET Core |[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2109019)|2019 年 10 月 29 日| 18.4|15.0.4573.2|

### <a name="features"></a>[機能]

| 機能 | 詳細 |
| :------ | :------ |
| 展開 | Azure SQL Data Warehouse (GA) に配置するためのサポートを追加します。 | 
| プラットフォーム | macOS、Linux、Windows 用の sqlpackage .NET Core GA。 | 
| Security | SHA1 コード署名を削除します。 |
| 展開 | 新しい Azure database エディションのサポートを追加: 汎用、BusinessCritical、ハイパースケール |
| 展開 | AAD ユーザーとグループの Managed Instance サポートを追加します。 |
| 展開 | .NET Core で sqlpackage の/AccessToken パラメーターをサポートします。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>既知の問題 

| 機能 | 詳細 |
| :------ | :------ |
| ScriptDom |  ScriptDom の解析回帰が18.3.1 で導入されました。 ' RENAME ' は、最上位のトークンとして正しく処理されないため、解析が失敗します。 これは、次の sqlpackage リリースで修正されます。 | 
| &nbsp; | &nbsp; |

### <a name="known-issues-for-net-core"></a>.NET Core に関する既知の問題

| 機能 | 詳細 |
| :------ | :------ |
| [インポート] |  圧縮されたファイルのサイズが 4 GB を超える bacpac ファイルの場合は、.NET Core バージョンの sqlpackage を使用してインポートを実行することが必要になる場合があります。  この動作は、.net Core が zip ヘッダーを生成する方法です。これは有効ですが、.NET Framework バージョンの sqlpackage では読み取ることができません。 | 
| 展開 | パラメーター/p: Storage = File はサポートされていません。 .NET Core では、メモリのみがサポートされています。 | 
| Always Encrypted | sqlpackage .NET Core は Always Encrypted 列をサポートしていません。 | 
| Security | sqlpackage .NET Core では、multi-factor authentication の/ua パラメーターはサポートされていません。 | 
| 展開 | json データによるシリアル化を使用している古い V2 .dacpac ファイルと .bacpac ファイルがサポートされません。 |
| &nbsp; | &nbsp; |

## <a name="1831-sqlpackage"></a>18.3.1 sqlpackage

|プラットフォーム|ダウンロード|リリース日|Version|ビルド
|:---|:---|:---|:---|:---|
|Windows|[MSI インストーラー](https://go.microsoft.com/fwlink/?linkid=2102893)|2019 年 9 月 13 日|18.3.1|15.0.4538.1|
|macOS .NET Core (プレビュー)|[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2102894)|2019 年 9 月 13 日| 18.3.1|15.0.4538.1|
|Linux .NET Core (プレビュー)|[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2102978)|2019 年 9 月 13 日| 18.3.1|15.0.4538.1|
|Windows .NET Core (プレビュー)|[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2102979)|2019 年 9 月 13 日| 18.13.1|15.0.4538.1|

### <a name="features"></a>[機能]

| 機能 | 詳細 |
| :------ | :------ |
| 展開 | Azure SQL Data Warehouse (プレビュー) に配置するためのサポートを追加します。 | 
| 展開 | /P: DatabaseLockTimeout = (INT32 ' 60 ') パラメーターを sqlpackage に追加します。 | 
| 展開 | /P: LongRunningCommandTimeout = (INT32) パラメーターを sqlpackage に追加します。 |
| エクスポート/抽出 | /P: TempDirectoryForTableData = (STRING) パラメーターを sqlpackage に追加します。 |
| 展開 | 配置コントリビューターを他の場所から読み込むことを許可します。 配置コントリビューターは、配置されている対象の dacpac と同じディレクトリ、sqlpackage のバイナリに関連する拡張機能のディレクトリ、および sqlpackage に追加される/p: AdditionalDeploymentContributorPaths = (STRING) パラメーターから読み込まれます。追加のディレクトリの場所を指定できます。 |
| 展開 | OPTIMIZE_FOR_SEQUENTIAL_KEY のサポートを追加します。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細 |
| :-- | :------ |
| 展開 | 自動インデックスが配置時に削除されないように、自動インデックスを無視するように修正しました。 | 
| Always Encrypted | Always Encrypted varchar 列の処理を修正します。 | 
| ビルド/配置 | Xml 列セットの nodes () メソッドを解決するように修正します。| 
| ScriptDom | ' URL ' 文字列が最上位レベルのトークンとして解釈された場合の追加の問題を修正します。 | 
| グラフ | 制約内の擬似列参照に対して生成された TSQL を修正しました。  | 
| [エクスポート] | 複雑さの要件を満たすランダムなパスワードを生成します。 | 
| 展開 | 制約を取得するときにコマンドタイムアウトを優先するように修正します。 | 
| .NET Core (プレビュー) | ファイルへの診断ログの記録を修正します。 | 
| .NET Core (プレビュー) | ストリーミングを使用して、大きなテーブルをサポートするテーブルデータをエクスポートします。 | 
| &nbsp; | &nbsp; |

## <a name="182-sqlpackage"></a>18.2 sqlpackage

|プラットフォーム|ダウンロード|リリース日|Version|ビルド
|:---|:---|:---|:---|:---|
|Windows|[MSI インストーラー](https://go.microsoft.com/fwlink/?linkid=2087429)|2019 年 4 月 15 日|18.2|15.0.4384.2|
|macOS .NET Core (プレビュー)|[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2087247)|2019 年 4 月 15 日 | 18.2 |15.0.4384.2|
|Linux .NET Core (プレビュー)|[zip ファイル](https://go.microsoft.com/fwlink/?linkid=2087431)|2019 年 4 月 15 日 | 18.2 |15.0.4384.2|

### <a name="features"></a>[機能]

| 機能 | 詳細 |
| :------ | :------ |
| グラフ | グラフ テーブルのエッジ制約とエッジ制約句のサポートが追加されました。 |
| 展開 | SQL Server 2016 以降のインデックス キーで 32 列をサポートするためのモデルの検証規則が有効になりました。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細 |
| :-- | :------ |
| 展開 | サポートされていないクエリ ヒントの使用に起因する SQL Server 2016 RTM データベースのリバース エンジニア リングが修正されました。 |
| 展開 | filegroup ステートメントの作成前に発生するように auto close alter ステートメントの配置順序が修正されました。 |
| ScriptDom | 'URL' 文字列が最上位レベルのトークンとして解釈されていた ScriptDom の回帰解析が修正されました。 |
| 展開 | alter table add index ステートメントの解析時の null 参照例外が修正されました。 | 
| スキーマ比較 | null 許容の保存される計算列でのスキーマ比較で、常に一致しないとなっていた結果が修正されました。|
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>18.1 sqlpackage

リリース日: &nbsp; 2019 年 2 月 1 日  
ビルド: &nbsp; 15.0.4316.1  
プレビュー リリース。

### <a name="features"></a>[機能]

| 機能 | 詳細 |
| :------ | :------ |
| 展開 | UTF8 照合順序のサポートが追加されました。 |
| 展開 | インデックス付きビューでの非クラスター化列ストア インデックスが有効になりました。 |
| プラットフォーム | .NET Core 2.2 に移動しました。 | 
| スキーマ比較 | .NET Core でのスキーマ比較でメモリ ストレージが使用されます。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細 |
| :-- | :------ |
| パフォーマンス | リバース エンジニアリング クエリでのレガシ カーディナリティ推定機能を使用するためのパフォーマンスが改善されました。 | 
| パフォーマンス | スクリプトを生成する際のスキーマ比較での顕著なパフォーマンス問題が修正されました。 | 
| スキーマ比較 | 特定の拡張イベント (xevent) セッションを無視するスキーマのドリフト検出ロジックが修正されました。 |
| グラフ | グラフ テーブルのインポート順序が修正されました。 | 
| [エクスポート] | オブジェクトのアクセス許可による外部テーブルのエクスポートが修正されました。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>既知の問題

このリリースには、.NET Core 2.2 をターゲットとする sqlpackage のクロスプラットフォーム プレビュー ビルドが含まれています。 sqlpackage は、macOS および Linux で実行できます。

| 既知の問題 | 詳細 |
| :---------- | :------ |
| 展開 | .NET Core では、ビルド コントリビューターと配置コントリビューターがサポートされません。 | 
| 展開 | .NET Core では、json データによるシリアル化を使用している古い .dacpac ファイルと .bacpac ファイルがサポートされません。 | 
| 展開 | .NET Core では、大文字と小文字が区別されるファイル システムの問題により、参照された .dacpacs (master.dacpac など) が解決されない場合があります。 | 回避策は、参照ファイルの名前をすべて大文字にすることです (例: MASTER.BACPAC)。 |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

リリース日: &nbsp; 2018 年 10 月 24 日  
ビルド: &nbsp; 15.0.4200.1

### <a name="features"></a>[機能]

| 機能 | 詳細 |
| :------ | :------ |
| 展開 | データベース互換性レベル 150 のサポートが追加されました。 | 
| 展開 | マネージ インスタンスのサポートが追加されました。 | 
| パフォーマンス | データベース操作の並列処理の程度を指定する MaxParallelism コマンドライン パラメーターが追加されました。 | 
| Security | SQL Server に接続するときの認証トークンを指定する AccessToken コマンドライン パラメーターが追加されました。 | 
| [インポート] | インポートでの BLOB/CLOB データ型のストリーミングのサポートが追加されました。 | 
| 展開 | スカラー UDF 'INLINE' オプションのサポートが追加されました。 | 
| グラフ | グラフ テーブルの 'MERGE' 構文のサポートが追加されました。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細 |
| :-- | :------ |
| グラフ | グラフ テーブルの解決されない擬似列が修正されました。 |
| 展開 | メモリ最適化テーブル使用時のメモリ最適化されたファイル グループによるデータベースの作成が修正されました。 |
| 展開 | 外部テーブルでの拡張プロパティの包含が修正されました。 |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

リリース日: &nbsp; 2018 年 6 月 22 日  
ビルド: &nbsp; 14.0.4079.2

### <a name="features"></a>[機能]

| 機能 | 詳細 |
| :------ | :------ |
| 診断 | SqlClient の例外メッセージを含めて、接続エラーのエラー メッセージが改良されました。 |
| 展開 | 単一パーティション インデックスのインポート/エクスポートで、インデックスの圧縮がサポートされます。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細 |
| :-- | :------ |
| 展開 | SQL 2017 以降での XML 列セットのリバース エンジニアリング問題が修正されました。 | 
| 展開 | データベース互換性レベル 140 のスクリプトが Azure SQL Database で無視される問題が修正されました。 |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

リリース日: &nbsp; 2018 年 1 月 25 日  
ビルド: &nbsp; 14.0.3917.1

### <a name="features"></a>[機能]

| 機能 | 詳細 |
| :------ | :------ |
| インポート/エクスポート | 入れ子になったステートメントの数が多い Transact-SQL を解析するための ThreadMaxStackSize コマンドライン パラメーターが追加されました。 |
| 展開 | データベース カタログ照合順序のサポート。 | 
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細 |
| :-- | :------ |
| [インポート] | Azure SQL Database の .bacpac をオンプレミスのインスタンスにインポートする際の、"_パスワードのないデータベース マスター キーは、このバージョンの SQL Server ではサポートされていません_" に起因するエラーが修正されました。 |
| グラフ | グラフ テーブルの解決されない擬似列エラーが修正されました。 |
| スキーマ比較 | スキーマを比較するための SQL 認証を修正します。 | 
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

リリース日: &nbsp; 2017 年 12 月 12 日  
ビルド: &nbsp; 14.0.3881.1

### <a name="features"></a>[機能]

| 機能 | 詳細 |
| :------ | :------ |
| 展開 |  SQL 2017 以降と Azure SQL Database での_テンポラル保持ポリシー_のサポートが追加されました。 | 
| 診断 | 診断情報を保存するファイル パスを指定する /DiagnosticsFile:"C:\Temp\sqlpackage.log" コマンドライン パラメーターが追加されました。 | 
| 診断 | 診断情報をコンソールにログ記録する /Diagnostics コマンドライン パラメーターが追加されました。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細 |
| :-- | :------ |
| 展開 | 認識できないデータベース互換性レベルに遭遇してもブロックは行われません。 代わりに、最新の Azure SQL Database またはオンプレミスのプラットフォームであるとみなされます。 |
| &nbsp; | &nbsp; |
