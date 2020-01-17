---
title: SQL Server Data Tools (SSDT) リリース ノート | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 08/15/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 9f4fa51ff0ba9a5ce3e2960ab07e3e1994ddb881
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874891"
---
# <a name="release-notes-for-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) リリース ノート

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

これらのリリース ノートは、Visual Studio (VS) 用 [SQL Server Data Tools (SSDT)](download-sql-server-data-tools-ssdt.md) に関するものです。

<!--
Hello.  We have switched to a newer standardized format for Release Notes articles.
Basically we have switched from bullet lists to a 2-column table.
And we have shortened the H2 titles, to reduce wrapping in the rightNav.
And we have renamed the .md file to the standard format, from 'changelog-for-sql-server-data-tools-ssdt.md' to 'release-notes-ssdt.md'.
The presently latest H2 section (## 15.9.0) has been converted to the new format.
But the older sections are too numerous and long to warrant conversion.

REQUEST_1:  Please use the newer 2-column table format from now onward, for each new release section.

REQUEST_2:  Please consider whether it is time to erase perhaps the oldest 25% of these H2 sections.
Or maybe move all but the latest 9 (of 25) H2 sections to a new file perhaps named 'release-notes-history-ssdt.md', and link to it from the bottom of this file.

For questions, contact CraigG or SStein or GeneMi.

GeneMi , 2019/03/22.

P.S.  There is no need to keep this large HTML comment indefinitely.
-->

## <a name="1592nbsp-ssdt-for-vs-2017"></a>15.9.2、&nbsp; VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2019 年 7 月 17 日  
_ビルド番号:_ &nbsp; 14.0.16194.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

| 新しい項目 | 詳細 |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integration Services (SSIS) | AzureEnabled 機能を追加しました。 Azure Data Factory で、プロジェクトのパッケージを SSIS のサービスとしてのプラットフォーム (PaaS) で実行できるようにしました |
| Integration Services (SSIS) | Oracle コネクタのプロパティを変数式から設定できない問題を修正しました |
| Integration Services (SSIS) | SQL Server 2019 より前を対象とするパッケージをデバッグするときに Oracle コネクタで VS_NEEDSNEWMETATDATA エラーが発生する問題を修正しました |
| Integration Services (SSIS) | パッケージ/プロジェクトで接続マネージャーのプロパティに式を使用している場合に、Oracle コネクタがパッケージ/プロジェクトのアップグレード/ダウングレードに失敗した問題を修正しました |
| Integration Services (SSIS) | Web サービス タスク エディターの [WSDL のダウンロード] ボタンが、TLS 1.1 & 1.2 プロトコルをサポートしていない問題を修正しました (対象は SQL Server 2019) |
| Integration Services (SSIS) | DQS 接続マネージャーを含むパッケージを保存後に再度読み込むことができない問題を修正しました |

### <a name="known-issues"></a>既知の問題

| 既知の問題 | 詳細 |
| :---------- | :------ |
| ExecuteOutOfProcess が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 | この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。 |
| SSDT for Visual Studio 2017 (15.8 以降) では、Teradata のソース/変換先を含むパッケージを設計することはサポートされていません。 | SSDT for Visual Studio 2017 (15.8) を使用します。 |
| パッケージ配置モデルのデータ ソースを作成または編集できません。 | データ ソース ウィザードを開くことができません。 |
| SSIS と SSAS が同じ Visual Studio インスタンスにインストールされている場合、Power Query ソースは OData v4 をサポートしない可能性があります。 | &nbsp; |
| SSIS と SSAS が同じ Visual Studio インスタンスにインストールされている場合、Power Query ソースでは Oracle への接続に ODBC を使用できない可能性があります。 | &nbsp; |
| Power Query ソースはローカライズされていません | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1591nbsp-ssdt-for-vs-2017"></a>15.9.1、&nbsp; VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2019 年 4 月 27 日  
_ビルド番号:_ &nbsp; 14.0.16191.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

| 新しい項目 | 詳細 |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integration Services (SSIS) | 以前のバージョンの SQL Server を対象にするとパッケージ パーツを正しく永続化できないという問題を修正しました。 |
| Integration Services (SSIS) | パッケージ パーツを使用する場合に、優先順位制約に式を追加できないという問題を修正しました。 |
| Integration Services (SSIS) | Power Query ソースおよび接続マネージャーの [ヘルプ] ボタンが正しいドキュメントにリンクしていないという問題を修正しました。 |
| Integration Services (SSIS) | VS ヘルプ ウィンドウに SSIS ビルド バージョンが表示されないという問題を修正しました。 |
| Integration Services (SSIS) | Ole DB およびフラット ファイル接続マネージャー用のプロパティ "ConnectByProxy" を追加しました。これにより、Azure-SSIS IR でセルフホステッド IR を使用してオンプレミスのデータへのアクセスを有効にすることができます。 |
| Integration Services (SSIS) | ODBC コンポーネントが DT_DBDATE データ型に誤ってマップされるという問題を修正しました。 |
| Integration Services (SSIS) | ADO.NET および OLE DB 接続マネージャー用のプロパティ "ConnectUsingManagedIdentity" を追加しました。これにより、Azure-SSIS IR 内でデータ ソースに接続するためのマネージド ID 認証を有効にすることができます。 |

### <a name="known-issues"></a>既知の問題

| 既知の問題 | 詳細 |
| :---------- | :------ |
| ExecuteOutOfProcess が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 | この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。 |
| SSDT for Visual Studio 2017 (15.8 以降) では、Teradata のソース/変換先を含むパッケージを設計することはサポートされていません。 | SSDT for Visual Studio 2017 (15.8) を使用します。 |
| パッケージ配置モデルのデータ ソースを作成または編集できません。 | データ ソース ウィザードを開くことができません。 |
| SSIS と SSAS が同じ Visual Studio インスタンスにインストールされている場合、Power Query ソースは OData v4 をサポートしない可能性があります。 | &nbsp; |
| SSIS と SSAS が同じ Visual Studio インスタンスにインストールされている場合、Power Query ソースでは Oracle への接続に ODBC を使用できない可能性があります。 | &nbsp; |
| Power Query ソースはローカライズされていません。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1590nbsp-ssdt-for-vs-2017"></a>15.9.0、&nbsp;VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2019 年 1 月 28 日  
_ビルド番号:_ &nbsp; 14.0.16186.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

| 新しい項目 | 詳細 |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integration Services (SSIS) | ADF 2017 の SSIS 用の Power Query ソース (プレビュー) を追加します。 |
| Integration Services (SSIS) | SQL Server 2012 のサポートが再び追加されます。 |
| Integration Services (SSIS) | SQL Server 2019 用の Oracle ソース/ターゲットを追加します。 |
| Integration Services (SSIS) | SQL Server 2019 をターゲットとする Oracle ソースとターゲットは、SSDT によって既にインストールされています。 <br/></br> 2017 以前のバージョンのサーバーをターゲットとするパッケージを設計するには、Microsoft ダウンロード サイトから該当する Oracle コネクターのバージョンをダウンロードして SSDT マシン上にインストールします。 <br/></br> [Attunity による SQL Server 2017 をターゲットとする Microsoft Connector Version 5.0 for Oracle ](https://www.microsoft.com/en-us/download/details.aspx?id=55179 ) <br/></br> [Attunity による SQL Server 2016 をターゲットとする Microsoft Connector Version 4.0 for Oracle ](https://www.microsoft.com/en-us/download/details.aspx?id=52950 )<br/></br> [Attunity による SQL Server 2014 をターゲットとする Microsoft Connector Version 3.0 for Oracle ](https://www.microsoft.com/en-us/download/details.aspx?id=44582 )<br/></br> [Attunity による SQL Server 2012 をターゲットとする Microsoft Connector Version 2.0 for Oracle ](https://www.microsoft.com/en-us/download/details.aspx?id=29283 ) |
| Integration Services (SSIS) | 以前のバージョンの SSIS から移行する際に、スクリプト タスク/コンポーネントを読み込みできないという問題を修正します。 |
| Integration Services (SSIS) | Windows 7 SP1 および Windows 8.1 でデータ ビューアーが機能しないという問題を修正します。 |
| Integration Services (SSIS) | パッケージの保存時に Visual Studio がクラッシュすることがあるという問題を修正します。 |
| Integration Services (SSIS) | パッケージを実行できない場合がある問題を修正します。 |
| Integration Services (SSIS) | この問題は、次の両方の条件に該当する場合に発生します:< br />< br /> &bull;   保護レベルが EncryptSensitiveWithPassword である。< br /> &bull;   ターゲット サーバー バージョンが SQL Server 2017 より前である。          |
| Integration Services (SSIS) | 既定のフォントを使用した注釈が SSDT に表示されないという問題を修正します。 |
| Integration Services (SSIS) | ISDeploymentWizard で、SQL 認証、Azure Active Directory 統合認証、および Azure Active Directory パスワード認証がコマンド ライン モードでサポートされるようになります。 |

### <a name="known-issues"></a>既知の問題

| 既知の問題 | 詳細 |
| :---------- | :------ |
| ExecuteOutOfProcess が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 | この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。 |
| SSDT for Visual Studio 2017 (15.8 以降) では、Teradata のソース/変換先を含むパッケージを設計することはサポートされていません。 | SSDT for Visual Studio 2017 (15.8) を使用します。 |
| SSIS と SSAS が同じ Visual Studio インスタンスにインストールされている場合、Power Query ソースは OData v4 をサポートしない可能性があります。 | &nbsp; |
| SSIS と SSAS が同じ Visual Studio インスタンスにインストールされている場合、Power Query ソースでは Oracle への接続に ODBC を使用できない可能性があります。 | &nbsp; |
| Power Query ソースはローカライズされていません。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1582nbsp-ssdt-for-vs-2017"></a>15.8.2、&nbsp;VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2018 年 11 月 5 日  
_ビルド番号:_ &nbsp; 14.0.16182.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能
**SSIS:**

スクリプト タスク/Azure-SSIS へのフラット ファイル変換先が含まれるパッケージを含む SSIS プロジェクトを展開すると、パッケージで Azure-SSIS の実行が失敗する問題を修正しました。 

### <a name="known-issues"></a>既知の問題:

- ExecuteOutOfProcess が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。
- SSDT for Visual Studio 2017 (15.8.2) では、Oracle/Teradata のソース/変換先を含むパッケージを設計することはサポートされていません。 SSDT for Visual Studio 2017 (15.8) を使用します。

## <a name="1581nbsp-ssdt-for-vs-2017"></a>15.8.1、&nbsp;VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2018 年 9 月 27 日  
_ビルド番号:_ &nbsp; 14.0.16179.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

**SSIS:**

1. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] のサポートが追加されます。
2. SQL Server 2012 のサポートが削除されます。

### <a name="known-issues"></a>既知の問題:

- ExecuteOutOfProcess が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。
- スクリプト タスク/フラット ファイルの変換先が含まれるパッケージを含む SSIS プロジェクトを Azure-SSIS に展開すると、Azure-SSIS でのパッケージの実行が失敗します。
- SSDT for Visual Studio 2017 (15.8.1) では、Oracle/Teradata のソース/変換先を含むパッケージを設計することはサポートされていません。 SSDT for Visual Studio 2017 (15.8) を使用します。


## <a name="158nbsp-ssdt-for-vs-2017"></a>15.8、&nbsp;VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2018 年 9 月 5 日  
_ビルド番号:_ &nbsp; 14.0.16174.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

**SSIS:**

1. スクリプト タスクまたはコンポーネントを保存するとコンパイル エラーが発生する VS 15.8 の回帰を修正しました。
1. 配置ウィザードが動作しない VS 15.8 の回帰を修正しました。
1. ADO.NET 接続マネージャーでサード パーティの ADO.NET プロバイダーがサポートされない問題を修正しました。

**インストーラー:**

- Windows 10 に SSDT をインストールしているときに途中で再起動する機能を実装しました。


### <a name="known-issues"></a>既知の問題:

- ExecuteOutOfProcess が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。

## <a name="1571nbsp-ssdt-for-vs-2017"></a>15.7.1、&nbsp;VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2018 年 7 月 2 日  
_ビルド番号:_ &nbsp; 14.0.16167.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

**SSIS:**

- AS タスクで使用するための新しい Azure Government AAD 機関 (login.microsoftonline.us) のサポートが追加されます。
- ターゲット サーバーのバージョンが SQLServer2016 のときに AS 処理タスク UI に "メソッドが見つかりません" と表示される問題が修正されます。
- ターゲット サーバーのバージョンが SQLServer2012 のときに一部のパイプライン コンポーネントを実行できない問題が修正されます。

**インストーラー:**

- VS インスタンス リストをフィルター処理して、SSDT をインストールできないインスタンスを除外します。

### <a name="known-issues"></a>既知の問題:

- ExecuteOutOfProcess が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。
- Windows 10 に SSDT をインストールするときに、[新しい SQL Server Data Tools for Visual Studio 2017 インスタンスをインストールします] を選ぶと、"要求されたメタファイル操作はサポートされていません" で失敗します。 コンピューターを再起動し、SSDT インストーラーをもう一度起動して、インストールを続行してください。

## <a name="1570nbsp-ssdt-for-vs-2017"></a>15.7.0、&nbsp;VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2018 年 6 月 4 日  
_ビルド番号:_ &nbsp; 14.0.16165.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

**SSIS:**

- [オプション] ダイアログの *[Integration Services デザイナー]* ページが正しく表示されない問題を解決。  
- *[並べ替え変換エディター]* エディターに表示されるテキストの輝度比率問題を解決。  
- コンボボックスを編集しようとすると *[参照の解決]* ダイアログが消える問題を解決。  
- *[Hadoop 接続マネージャー]* の F1 ヘルプ リンクが機能しない問題を解決。  
- SQL Server 2016 が対象のとき、コンテナーに含まれていない場合、スクリプト タスク コードが失われる問題を解決。  


**インストーラー:**

- VS 15.7.2 で SSRS と SSIS をインストールする前に SSAS をインストールできない問題を解決。

### <a name="known-issues"></a>既知の問題:

- *ExecuteOutOfProcess* が *True* に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。

## <a name="1560nbsp-ssdt-for-vs-2017"></a>15.6.0、&nbsp;VS 2017 用 SSDT

_リリース済み:_ &nbsp; 2018 年 4 月 10 日  
_ビルド番号:_ &nbsp; 14.0.16162.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

**SSIS:**

- SQLServer2016 と SQLServer2017 を対象とする AS の処理タスクで処理手順のログが記録されない問題を修正しました
- SSDT で英語以外の長いタスク名の dtsx を開くとアクセス違反が発生する問題を修正しました
- ScriptTask の変数一覧がタスク UI に時々表示されなくなる問題を修正しました
- パッケージの場所が SQL Server である場合に既存のパッケージのコピーの追加が失敗する問題を修正しました
- 一部のエディターのダイアログ ボックスでコンボ ボックスにアクセスするとフォーカスがスタックする問題を修正しました。
- VS のテーマの切り替え中に背景が変化しない問題を修正しました。
- ダーク テーマで注釈と読み込み中のラベルが表示されない問題を修正しました。
- SSIS ツールボックスが無効なアイテムで状態プロパティが正しく定義されない問題を修正しました。
- WebServiceTask の実行が常に失敗する問題を修正しました。
- 接続文字列を式がプロジェクト パラメータに依存するように可変に設定すると、パッケージの展開が失敗する問題を修正しました。

**インストーラー:**

- プライバシーに関する免責事項に "SQL Server Data Tools のカスタマー エクスペリエンス向上プログラム" のリンクを追加します。
- [Install new SQL Server Data Tools for Visual Studio 2017 instance]\(Visual Studio 2017 インスタンス用の新しい SQL Server Data Tools のインストール\) を選択すると VS インストーラー ウィンドウが開く問題を修正しました

### <a name="known-issues"></a>既知の問題:
- ExecuteOutOfProcess が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。

## <a name="1552nbsp-ssdt-for-vs-2017"></a>15.5.2、&nbsp;VS 2017 用 SSDT

_ビルド番号:_ &nbsp; 14.0.16156.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

**SSIS**
- SSAS と SSIS の両方が同じ VS 2017 インスタンスにインストールされているときに、SSIS 2008 プロジェクトの移行が失敗する問題を修正しました。
- Rdlc レポート デザイナーと SSIS の両方が同じ VS 2017 インスタンスにインストールされているときに、Rdlc プロジェクトをビルドできない問題を修正しました。
- 注釈の色を更新できない問題を修正しました。
- Hadoop 接続マネージャー エディターで一部の文字列が他の言語で切り捨てられる問題を修正しました。
- OData 接続マネージャー エディターで一部の文字列が切り捨てられる問題を修正しました。
- Integration Services のプロジェクトのインポート ウィザード ウィンドウで一部の文字列が切り捨てられる問題を修正しました。
- SSIS ツール ボックス情報ウィンドウのタイトルの問題を修正しました。
- Integration Services のプロジェクトの配置ウィザード ウィンドウで一部の文字列が切り捨てられる問題を修正しました。 

**インストーラー**
- ペイロードのダウンロードが "指定されたファイルが見つかりません (0x80070002)" というエラーで失敗することがある問題を修正しました。  

### <a name="known-issues"></a>既知の問題
- *ExecuteOutOfProcess* が *True* に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。

## <a name="1551nbsp-ssdt-for-vs-2017"></a>15.5.1、&nbsp;VS 2017 用 SSDT

_ビルド番号:_ &nbsp; 14.0.16148.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

Visual Studio 2017 (15.5.1) はバージョン 15.5.0 と同じリリースですが、インストーラーの次のバグが修正されています。

1.  SQL Server Integration Services のインストールの後処理でインストーラーが応答を停止する問題を修正しました。
2.  次のエラー メッセージで設定が失敗する問題を修正します。「要求されたメタファイル操作はサポートされていません (0x800707D3)」

以上の 2 つのバグ修正に加え、15.5.0 の次の詳細が 15.5.1 にも当てはまります。

## <a name="1550nbsp-ssdt-for-vs-2017"></a>15.5.0、&nbsp;VS 2017 用 SSDT

_ビルド番号:_ &nbsp; 14.0.16146.0  
_Visual Studio 2017 用 SSDT。_

### <a name="whats-new"></a>新機能

SSDT for Visual Studio 2017 (15.5.0) がプレビューから一般公開 (GA) になりました。

**インストーラー**
1. セットアップ UI がローカライズされました。
1. アイコンが品質の良いものに変わりました。

**Integration Services (IS)**
1. ADF で Azure SSIS IR にデプロイするときのデプロイ ウィザードにパッケージ検証手順が追加されました。Azure SSIS IR で実行する SSIS パッケージの互換性問題を検出します。 詳細については、「[Azure にデプロイされた SSIS パッケージの検証](../integration-services/lift-shift/ssis-azure-validate-packages.md)」を参照してください。
1. SSIS 拡張機能がローカライズされました。

### <a name="bug-fixes"></a>バグの修正

**Integration Services (IS)**
1. OLEDB と ADO.NET の接続マネージャーのレイアウトが壊れる問題を修正しました。
2. ディメンション処理タスクを編集しようとすると、アセンブリが見つからないエラーが表示される問題を修正しました。

### <a name="known-issues"></a>既知の問題

ExecuteOutOfProcess が True に設定されていると、**Integration Services (IS)** SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。

## <a name="173nbsp-ssdt-for-vs-2015"></a>17.3、&nbsp;VS 2015 用 SSDT

_ビルド番号:_ &nbsp; 14.0.61712.050  
_Visual Studio 2015 用 SSDT。_

### <a name="whats-new"></a>新機能

**Analysis Services (AS) プロジェクト**
- 表形式プロジェクトに新しいオプションを 3 つ追加しました ([オプション]、[Analysis Services 表形式]、[データ インポート] の下):
  - レガシ データ ソースを有効にする - ユーザーは最新の互換性モードで以前の "1200 互換性モード" データ ソースを作成できます。
  - 型の自動検出 - 有効にすると、最新のデータ ソースのクエリ エディターは、非構造化クエリが読み込まれるとデータ型の検出を試行します。 検出に成功した場合、新しい手順がクエリに追加されることがあります。
  - バックグラウンド分析の実行 - 有効にすると、最新のデータ ソースのクエリ エディターは、クエリの出力スキーマを分析する目的で、クエリが読み込まれるとデータ ソースに対してクエリを実行します。

**Integration Services (IS)**
- ADF で Azure SSIS IR にデプロイするときのデプロイ ウィザードにパッケージ検証手順が追加されました。Azure SSIS IR で実行する SSIS パッケージの互換性問題を検出します。 詳細については、「[Azure にデプロイされた SSIS パッケージの検証](../integration-services/lift-shift/ssis-azure-validate-packages.md)」を参照してください。


### <a name="bug-fixes"></a>バグの修正

**Analysis Services (AS) プロジェクト:**
- TFS のモデル変更を確認するとき、ハンドルされていない例外を引き起こす可能性がある問題を修正しました。
- 複雑な M 式の表を 1400 モデルに追加するとき、例外を引き起こす可能性がある問題を修正しました。
- モデル ダイアグラム ビューでメタデータを検索するとき、Visual Studio でクラッシュを引き起こす可能性がある問題を修正しました。
- パーティション M クエリの変更を保存すると、計算済みの列を表の定義から削除することがあるという、1400 モデルの問題を修正しました。
- データの取得/テーブル エディター UI で 1400 モデルに [クエリ名の変更] を使用するとき、現在のデータ モデルとの互換性の検証中にフリーズする可能性がある問題を修正しました。
- Azure Analysis Service に 1400 モデルをデプロイするとき、Newtonsoft アセンブリ参照がなくなる問題を修正しました。
- 特定の状況で、1400 モデルに PQ 経由でデータをインポートするときにエラーを引き起こした問題を修正しました。
- Windows スケーリングを設定したときに表示される PowerQuery ユーザー インターフェイス ダイアログのスケーリング問題を修正しました。
- 名前変更ロールの問題を修正しました。
- 特定の状況で変更を適切に保存/同期しないという、プロジェクト構成の問題を修正しました。
- "型の変更" 手順を自動的に追加するという、PowerQuery の問題を修正しました。
- 統合ワークスペース モードに、または統合ワークスペース モードから切り替えた後、BIM ファイルを開けなくなる問題を修正しました。
- MaxConnections プロパティが表形式モデルのデータ ソースに表示されるようになりました。
- PowerQuery エディター ウィンドウの初期サイズを大きくしました。
- PowerQuery エディターで、"Source" など、M クエリ キーワードがローカライズされました。
- 編集する表ごとに同じ資格情報を入力しなくても済むように、1400 モデルと構造化データ ソースを使用するとき、資格情報をキャッシュします。

**RS プロジェクト:**
- マルチ レポート プロジェクトでシングル レポートをデプロイできない問題を修正しました。
- デプロイで問題を引き起こした可能性がある共有データ ソースの問題を修正しました。
- コード ビュー、デザイン ビュー、クエリ エディター ウィンドウを切り替えたときに元に戻すマネージャーをクラッシュさせた問題を修正しました。
- ランタイム エラー後、パラメーター ウィンドウが消える原因となった可能性がある問題を修正しました。
- ソース管理マッピングを失わせる可能性があった、レポート プロジェクトの問題を修正しました。

**Integration Services:**
- Analysis Services プロセス タスクで接続を切り替えるときに発生した可能性がある問題を修正しました。
- 一部のタスク/コンポーネントが正しくローカライズされていない問題を修正しました。
- \__$command\_id 列を追加する CDC に SQL 修正を適用した後、CDC コンポーネントが壊れる問題を修正しました。

## <a name="1540-previewnbsp-ssdt-for-vs-2017"></a>15.4.0 (プレビュー)、&nbsp;VS 2017 用 SSDT

_ビルド番号:_ &nbsp; 14.0.16134.0  
_Visual Studio 2017 用 SSDT。_
  
### <a name="whats-new"></a>新機能

このリリースでは、Visual Studio 2017 (15.4 以降) での SQL Server データベース、Analysis Services、Reporting Services、および Integration Services の各プロジェクトに対するスタンドアロン Web インストーラーが提供されています。

### <a name="installer"></a>インストーラー

- ユーザーは、VS2017 インスタンス用の新しい SSDT をインストールするときに、ニックネームを設定できるようになります。
- VS インスタンスが選ばれていない場合、インストーラーの機能選択ボックスが表示されなくなります。
- お客様のフィードバックに基づいて、インストーラーの一部のメッセージが修正されます。
- インストーラーがアップグレードに対応していない問題が修正されます。


### <a name="ssis"></a>SSIS

- Azure 機能パックがインストールされているときに Import/Export ウィザードがデータ ソースを一覧表示できない問題が修正されます。
- SSIS Analysis Services プロセス タスクを編集すると接続切り替え中に例外がスローされる問題が修正されます。
- __$command_id 列を追加する SQL の修正を適用した後、CDC コンポーネントが壊れる問題が修正されます。
- 使用していない SQL Server を対象にしたときに、サード パーティのパッケージを編集および実行できない問題を修正しました。
- DTSWizard.exe をダブルクリックして [フラット ファイル ソース] を選んだときに、フラット ファイル ソース構成ダイアログ ボックスが正しく表示されない問題が修正されます。
- SQL Server 2017 を対象にした場合に Azure Feature Pack のタスク/コンポーネントを含むパッケージが実行できない問題が修正されます。


**既知の問題**

- インストーラーはローカライズされていません。
- *ExecuteOutOfProcess* が True に設定されていると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。


## <a name="1730nbsp-ssdt-for-vs-2015"></a>17.30、&nbsp;VS 2015 用 SSDT

_ビルド番号:_ &nbsp; 14.0.61709.290  
_Visual Studio 2015 用 SSDT。_

### <a name="whats-new"></a>新機能

**Analysis Services (AS)**

- Cosmos DB と HDI Spark は 1400 モデルで有効です。
- 表形式データ ソースのプロパティ。
- 1400 互換性レベルのモデルのクエリ エディターで新しいクエリを作成する場合、"空のクエリ" がサポートされるようになりました。
- 1400 モード モデルのクエリ エディターで、新しいテーブルを自動的に処理することなく、クエリを保存できるようになりました。

**Reporting Services (RS)**

- プロジェクトで、構築と展開に MSBuild の使用をサポートするアップグレードされた形式を開くときに、メッセージが表示されるようになりました。

### <a name="known-issues"></a>既知の問題

**Analysis Services (AS)**

- パースペクティブがある直接クエリ モードの 1400 互換性レベルのモデルは、メタデータのクエリまたは検出に失敗します。

**Reporting Services (RS)**

- 新しいレポート プロジェクト形式は、ソース管理バインディングを保持せず、次のメッセージのようなエラーが発生します。

   *プロジェクト ファイル C:\path はソース管理にバインドされていませんが、ソリューションはソース管理のバインド情報を含んでいます。*
 
   この問題を回避するには、ソリューションを開くたびに **[ソリューション バインドを使用する]** をクリックします。

- プロジェクトを新しい MSBuild 形式にアップグレードした後に、次のようなメッセージで保存が失敗することがあります。

   *"パラメーター '{0}' を NULL にすることはできません。"*

   この問題を回避するには、 *[プロジェクト構成]* を更新し、 *[プラットフォーム]* プロパティを設定してください。

### <a name="bug-fixes"></a>バグの修正

**Analysis Services (AS)**

- 表形式モデル ダイアグラム ビューを読み込むときのパフォーマンスを大幅に改善しました。
- 複数の問題を修正し、1400 互換性レベル モデルの PowerQuery 統合とエクスペリエンスを改善しました。
   - ファイル ソースのアクセス許可を編集できない問題を修正しました。
   - ファイル ソースのソースを変更できない問題を修正しました。
   - ファイル ソースに不適切な UI が表示される問題を修正しました。
- "Join on Date (日付で結合)" リレーションシップが非アクティブなときに、"JoinOnDate" プロパティが削除される問題を修正しました。
- クエリ ビルダーの [新しいクエリ] オプションで、新しい空のクエリを作成できるようになりました。
- 既存のデータ ソース クエリに対する編集で、1400 互換性レベルのテーブルのモデル定義が更新されない問題を修正しました。
- 例外が発生する可能性があるカスタム コンテキスト式に関する問題を修正しました。
- 1400 表形式モデルで名前が重複する新しいテーブルをインポートするときに、競合する名前があるため、名前が一意になるように調整されたことが通知されるようになりました。
- 現在のユーザー権限借用モードは、サポートされないシナリオのため、インポート モードではモデルから削除されました。
- PowerQuery 統合は、追加のデータ ソースのオプション (OData.Feed、Odbc.DataSource、Access.Database、SapBusinessWarehouse.Cubes) をサポートするようになりました。
- PowerQuery のデータ ソースのオプション文字列には、クライアントのロケールに基づいてローカライズされたテキストが正しく表示されるようになります。
- ダイアグラム ビューには、1400 互換性レベル モデルで M クエリ エディターから新しく作成された列が表示されるようになりました。
- Power Query エディターには、データをインポートしないオプションが追加されました。
- VS2017 の多次元モデルが Oracle からテーブルをインポートするときに使用されるデータ カートリッジのインストールに関する問題を修正しました。
- マウス カーソルが表形式の数式バーを離れるときに、クラッシュが発生する可能性がある問題を修正しました。
- テーブル名を変更することで、ソース テーブルが不適切に変更され、予期しないエラーが発生する [テーブルのプロパティの編集] ダイアログの問題を修正しました。
- 多次元プロジェクトのロール デザイナーのセル データ タブ デザイナーで [キューブのセキュリティをテスト] を呼び出そうとすると、VS2017 で発生する可能性があるクラッシュを修正しました。
- SSDT:データ ソースが表形式の場合、プロパティは編集できません。
- ソリューション ファイルで、MSBuild と DevEnv ビルドが正しく動作しなくなる場合がある問題を修正しました。
- 表形式モデルに大きなメタデータが含まれる場合、モデルの変更 (メジャーの DAX 編集、計算された列) をコミットするときのパフォーマンスが大幅に改善されました
- 1400 互換性レベル モデルで PowerQuery を使用してデータをインポートする場合に関するいくつかの問題を修正しました
   - [インポート] をクリックした後にインポートに時間がかかり、UI に状態が表示されない
   - ナビゲーション ビューでインポートするテーブルを選択しようとするときに、大きなテーブルのリストが非常に遅くなる
   - クエリ エディター ビューで 35 個のクエリのリストがあると、クエリ エディターのパフォーマンスが低下する (PBI デスクトップの問題でもあります)
   - 特定の場合に、複数のテーブルをインポートするとツールバーが無効になり、インポートが完了しないことがある 
   - PQ を使用してテーブルをインポートした後に、モデル デザイナーが無効と表示され、データが表示されない
   - PQ UI で [新しいテーブルの作成] をオフにしても、新しいテーブルが作成される
   - フォルダー データ ソースが資格情報の入力を求めない 
   - オブジェクト参照で、構造化されたデータ ソースで更新された資格情報の取得を試行することができる例外が設定されない
   - M 式が含まれるパーティション マネージャーを開くと、処理が非常に遅くなる
   - PQ エディターでテーブルのプロパティを選択しても、プロパティが表示されない
- 最上位の例外をキャッチし、[出力] ウィンドウに表示する Power Query UI 統合の保全性を改善しました
- コンテキスト式の場合に、データ ソースの構造で変更が維持されない ChangeSource に関する問題を修正しました
- M 式のエラーによって、エラー メッセージが表示されずにモデルの更新に失敗することがある問題を修正しました
- "ソリューションを閉じる前にビルドを中止しなければなりません" エラーで SSDT が終了する問題を修正しました
- 1400 互換性レベル モデルで不適切な権限借用モードを設定すると、VS が応答を停止したような状態になる問題を修正しました 
- 詳細な行プロパティは、空ではない場合にのみ、JSON にシリアル化されるようになります (既定からの変更)
- Oracle OLEDB ドライバーは、表形式の直接クエリ モードのリストで使用できるようになりました
- 1400 互換性表形式モデルに M 式を追加すると、表形式モデル エクスプローラー (TME) で表示または更新できるようになりました
- 1400 よりも前の互換性レベル モデルで "その他" のデータ ソースを使用してインポートしようとすると、MSOLAP プロバイダーが VS2017 に表示されなくなる問題を修正しました
- TME を介して変換を追加すると発生する可能性がある問題を修正しました 
- 特定の場合にタブが不適切に表示または非表示になるオブジェクト レベル セキュリティ インターフェイスの問題を修正しました
- [データベースへの接続] ダイアログを使用して以前に読み込んだ多次元モデルを開こうとすると、エラーが発生する可能性がある問題を修正しました
- 多次元モデルにカスタム アセンブリを追加するときにエラーが発生する問題を修正しました

**Reporting Services (RS)**

- VS 2017 の RDLC のコンパイルとビルドに関する問題を修正しました

## <a name="1530-previewnbsp-ssdt-for-vs-2017"></a>15.3.0 (プレビュー)、&nbsp;VS 2017 用 SSDT

_ビルド番号:_ &nbsp; 14.0.16121.0  
_Visual Studio 2017 用 SSDT。_
  
### <a name="whats-new"></a>新機能

このプレビューは、SSDT for Visual Studio 2017 の最初のバージョンです。 このリリースでは、Visual Studio 2017 (15.3 以降) での SQL Server データベース、Analysis Services、Reporting Services、および Integration Services のプロジェクトに対してスタンドアロン Web インストール エクスペリエンスを導入します。


**既知の問題**

- インストーラーはローカライズされていません。
- SSIS はローカライズされていません。
- *ExecuteOutofProcess* が *True* に設定されると、SSIS パッケージ実行タスクはデバッグをサポートしません。 この問題はデバッグにのみ該当します。 DTExec.exe または SSIS カタログを介した保存、展開、実行は影響を受けません。
- サード パーティの拡張機能を含む SSIS パッケージは、その他のサーバー バージョンを対象にするように切り替えることはできません。


## <a name="172nbsp-ssdt-for-vs-2015"></a>17.2、&nbsp;VS 2015 用 SSDT

_ビルド番号:_ &nbsp; 14.0.61707.300  
_Visual Studio 2015 用 SSDT。_

### <a name="whats-new"></a>新機能


**AS プロジェクト:**
- 1400 互換性レベル表形式モデルでの高度なセキュリティの *[ロール]* ダイアログでオブジェクト レベルのセキュリティを構成できるようになりました。
- VS2017 の SSDT AS プロジェクトの AS Azure モデルにメール アドレスがないユーザーに対する新しい AAD ロール メンバー選択。
- ADAL 資格情報のキャッシュ動作をカスタマイズするための SSDT AS テーブル プロジェクトでの新しい AS Azure の "Always Prompt" プロジェクト プロパティ。


### <a name="bug-fixes"></a>バグの修正

**全般**
- SQL Server 2017 の参照のブランド化が更新されました。

**AS プロジェクト**
- DAX メジャーの変更とその他のモデルの編集をコミットするときのエクスペリエンスを向上させるため、大幅なパフォーマンスの修正が行われました。
- 1400 互換性レベル表形式モデルを使用する Analysis Services プロジェクトでの Power Query 統合で複数の問題を修正しました。
- VS2017 でデザイン集計デザイナーのみが読み込みに失敗する場合がある、多次元プロジェクトの問題を修正しました。
- Analysis Services 多次元 DSV ダイアグラムで項目をドラッグしたときに VS 2017 がクラッシュする場合がある問題を修正しました。
- [展開] ダイアログが Visual Studio の上のフォアグラウンドに常に表示されない AS プロジェクトの問題を修正しました。
- Data Marketplace から Analysis Services をデータ ソースとしてインポートするのは、サービスが停止されたため、削除されました。
- 表形式モデル エクスプローラーで既存のデータ ソースから新しいテーブルのインポート後に、テーブル デザイナーが無効になったままになる問題を修正しました。
- [モデル] メニュー項目で [データ ソースからのインポート] または [データ ソースの追加] が間違ったコンテキストで非表示のままになる問題を修正しました。
- フォーカスがメジャーを作成するために使用された列に戻るのを避けるため、表形式モデル エクスプローラーからメジャーを作成する際のエクスペリエンスが向上しました。
- AS の表形式プロジェクトの統合ワークスペースから明示的ワークスペース サーバーに切り替えると、古いデータベース ファイルにクリーンアップされるようになりました。
- [行レベルセキュリティ] チェックボックス UI の状態が、基になるオブジェクトの実際の状態に関係なく、最初はオフになっている、AS 表形式 1400 モデル プロジェクトの問題を修正しました。
- Power Query を使用してテキスト ファイルまたは Excel ファイルを 1400 互換モード表形式モデルにインポートして、ハンドルされない例外が発生した場合に、クラッシュが発生することがある問題を修正しました。
- AS 表形式モデル デザイナーの DAX 数式の編集コントロール内のスクロールバーのつまみで発生することがある問題を修正しました。
- PowerQuery マッシュアップ データ ソースにユーザー名認証またはパスワード認証が含まれていると、変更できない問題を修正しました。
- 接続文字列に追加のプロパティを設定するときに、データ ソースの接続を妨げる可能性のある問題を修正しました。
- 複数の AS 表形式モデル プロジェクトが読み込まれるときに、最初にデザイナー内のいずれともやり取りをすることなく、2 番目のモデル デザイナーが閉じて VS がクラッシュする可能性がある問題を修正しました。
- KPI の書式設定に対して行った編集が保持されない場合がある問題を修正しました。
- 数式バーが表示されたかどうかについて、メニューのチェック状態が正しく表示されない PowerQuery UI の問題を修正しました。
- 表形式モデル エクスプローラーから [データ ソースの変更] メニューを選択すると、VS がクラッシュすることがある PowerQuery データソースを使用した AS 表形式 1400 互換性レベル プロジェクトの問題を修正しました。
- 1400 表形式モデルの読み込み時に、"*ファイルまたはアセンブリ 'Microsoft.ProBI.MashupLibrary' を読み込むことができませんでした*" というエラーが表示されることがある断続的な問題を修正しました。

**RS プロジェクト**
- RS ルーラーとパラメーター ボックスの設定に対するユーザーの選択は、セッション間で正しく記憶されます。

**IS プロジェクト**
- ADO/ADO.NET ForEachLoop コンテナーが正しく表示されない問題を修正しました
- 一部のタスク/コンポーネント/ウィザードがローカライズされていない問題を修正しました
- 最新の *TargetServerVersion* が "SQL Server vNext" から "SQL Server 2017" に変更されました

## <a name="1710nbsp-ssdt-for-vs-2015"></a>17.10、&nbsp;VS 2015 用 SSDT

_ビルド番号:_ &nbsp; 14.0.61705.170  
_Visual Studio 2015 用 SSDT。_

### <a name="whats-new"></a>新機能
**AS プロジェクト:**
- ユーザーは、1400 モデルの UI の列にエンコーディング ヒントを設定できます。
- モデルに関係がない IntelliSense をオフライン モードで使えるようになりました
- 表形式モデル エクスプローラーにモデル (1400 互換性レベル表形式モデル) 全体で利用可能な名前付き M 式を表すノードが含まれるようになりました
- Microsoft Azure Portal の IAM に似た Azure Active Directory ユーザー選択ウィンドウを、表形式モデルでロール メンバーを設定するときに使えるようになりました

**データベース プロジェクト:**
- DacFx 17.1 に更新されました

### <a name="bug-fixes"></a>バグの修正
- VS2017 の Visual Studio オプションでビジネス インテリジェンス デザイナー グループ名が正しく表示されない問題を修正しました
- レポート プロジェクトまたは AS プロジェクトでソリューションのコード マップを生成するときにクラッシュが発生する可能性がある問題を修正しました
- Analysis Services 1400 互換性レベル表形式モデルの PowerQuery 統合でのいくつかの問題を修正しました
- メジャーを定義するときに代入演算子が新しい行にならない新しい DAX エディター ツール ウィンドウでの問題を修正しました
- パースペクティブ内のメジャーの名前を変更するときに、テーブル メジャーの表示が更新されない問題を修正しました
- Analysis Services 統合ワークスペース エンジンとテーブル オブジェクト モデルを更新し、翻訳を含む 1200 テープル プロジェクトが SQL Server 2016 Analysis Services サーバーへの配置で失敗する原因となったバグ再発を修正しました
- 新しい 1400 テーブル データ ソースの作成/削除が非常に遅くなるパフォーマンスの問題を修正しました
- 異なる DSV 間ですばやくビューを変更すると多次元モデルの DSV ダイアグラムがレンダリングを停止する問題を修正しました

## <a name="dacfx-171"></a>DacFx 17.1

- 他の ID 列でメモリ最適化テーブルの列を暗号化するときの問題を修正しました
- CREATE DATABASE の CATALOG_COLLATION オプションの SQLDOM のサポート

## <a name="dacfx-1701"></a>DacFx 17.0.1

- EKM プロバイダー [Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/3132749/sqlpackage-exe-fails-when-extracting-a-database-which-contains-an-asymmetric-key-using-an-ekm-provider)での HSM による非対称キーでのデータベースの問題を解決しました

## <a name="170nbsp-ssdt-for-vs-2015"></a>17.0、&nbsp;VS 2015 用 SSDT

_ビルド番号:_ &nbsp; 14.0.61704.140  
_Visual Studio 2015 用 SSDT。_  
_SQL Server 2017 までのサポート。_

### <a name="whats-new"></a>新機能
**データベース プロジェクト:**
- ビューのクラスター化インデックスが修正され、展開がブロックされることはなくなりました
- 列の暗号化に関連するスキーマ比較文字列で、インスタンス名ではなく適切な名前が使用されます。   
- SqlPackage に新しいコマンド ライン オプション(ModelFilePath) が追加されました。  これにより、上級ユーザーは、インポート、発行およびスクリプト作成操作で、外部 model.xml を指定することができます   
- Azure AD ユニバーサル認証と多要素認証 (MFA) をサポートするように DacFx API が拡張されました

**IS プロジェクト:**
- SSIS OData ソースと OData 接続マネージャーで、Microsoft Dynamics AX Online と Microsoft Dynamics CRM Online の OData フィードに接続できるようになりました。
- SSIS プロジェクトが "SQL Server 2017" のターゲット サーバー バージョンをサポートするようになりました 
- SQL Server 2017 をターゲットにした場合、CDC 制御タスク、CDC スプリッター、および CDC ソースをサポートします。 

**AS プロジェクト:**
- Analysis Services PowerQuery 統合 (1400 互換性レベル表形式モデル):
    - DirectQuery は、SQL Oracle で使用でき、サード パーティ製のドライバーがインストールされている場合は Teradata で使用できます
    - PowerQuery での例示による列の追加
    - 1400 モデルでのデータ アクセス オプション (M エンジンによって使われるモデル レベルのプロパティ)
        - 高速結合の有効化 (既定値は false です。true に設定すると、マッシュアップ エンジンはデータを結合するときにデータ ソースのプライバシー レベルを無視します)
        - 従来のリダイレクトの有効化 (既定値は false です。true に設定すると、マッシュアップ エンジンは安全ではない可能性のある HTTP リダイレクトに従います。  たとえば、HTTPS から HTTP URI へのリダイレクト)  
        - エラー値を null として返します (既定値は false です。true にすると、セル レベルのエラーが null として返されます。 false の場合、セルにエラーが含まれると例外が発生します)  
    - PowerQuery を使う追加データ ソース (ファイル データ ソース)
        - [エクスポート] 
        - テキスト/CSV 
        - Xml 
        - Json 
        - フォルダー 
        - Access データベース 
        - Azure Blob Storage 
    - ローカライズされた PowerQuery ユーザー インターフェイス
- DAX エディター ツール ウィンドウ
    - SSDT の [表示] > [その他のウィンドウ] メニューで利用可能な DAX 編集エクスペリエンスがメジャー、計算列、詳細行の式に関して改良されました
    - DAX パーサー\Intellisense の機能強化


**RS プロジェクト:**
- 埋め込み可能な RVC コントロールで SSRS 2016 をサポートできるようになりました。

### <a name="bug-fixes"></a>バグの修正
**AS プロジェクト:**
- BI プロジェクトのテンプレートの優先順位を修正して、VS の [新しいプロジェクト] カテゴリで先頭に表示されることがないようにしました
- SSIS、SSAS、または SSRS ソリューションが開いているとき、めったにない状況で発生する可能性がある VS のクラッシュを修正しました
- 表形式: DAX の解析と数式バーにさまざまな機能強化とパフォーマンス修正を行いました。
- 表形式:SSAS 表形式プロジェクトが開いていない場合、表形式モデル エクスプローラーが表示されなくなりました。
- 多次元:高 DPI コンピューターで処理中のダイアログを使用できない問題を修正しました。
- 表形式:SSMS が既に開いている場合に BI プロジェクトを開くと SSDT で障害が発生する問題を修正しました。( [Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/3100900/ssdt-faults-when-opening-any-bi-project-when-ssms-is-already-open)を参照)。
- 表形式: 1103 モデルの bim ファイルに階層が正しく保存されない問題を修正しました ([Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/3105222/vs-2015-ssdt)を参照)
- 表形式: 32 ビット コンピューターで、サポートされていない統合ワークスペース モードが使用できる問題を修正しました。
- 表形式:半選択モード (DAX 式は入力したが、メジャーをクリックしている場合など) の状態で何かをクリックするとクラッシュする可能性がある問題を修正しました。
- 表形式:展開ウィザードでモデルの .Name プロパティが "Model" にリセットされる問題を修正しました ( [Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/3107018/ssas-deployment-wizard-resets-modelname-to-model)を参照)。
- 表形式:ダイアログ ビューが選択されていない場合でも、TME で階層を選択するとプロパティが表示される問題を修正しました。
- 表形式:特定のアプリケーションから貼り付ける場合、DAX 数式バーに、テキストではなく、イメージまたは他のコンテンツが貼り付けられる問題を修正しました。
- 表形式:特定の定義のメジャーが存在するため、1103 の一部の古いモデルが開けない問題を修正しました。
- 表形式:XEvent セッションを削除できない問題を修正しました。
- devenv.com で AS "smproj" ファイルのビルドを試行すると失敗する問題を修正しました
- 韓国 IME での表形式モデルのシート タブのタイトル テキストが何度も変更されるという問題を修正して、テキストを確定しました。
- DAX Related() 関数の Intellisense が正常に機能せず、他のテーブルの列が表示されない問題を修正しました。
- データベースからの AS テーブル プロジェクトのインポートを、AS データベースの一覧を並べ替えることで改善しました。
- AS 表形式モデルで計算テーブルを作成するときに、候補オブジェクトとしてテーブルが式に表示されない問題を修正しました
- コードの表示後に統合ワークスペースを使用して プレビュー 1400 AS モデルを開こうとしたときに発生する問題を修正しました。
- 特定の状況で (初期カタログではサポートされていない) 一部のデータ ソースの正常な動作を妨げていた問題を修正しました。 
- デプロイ ウィザードは、パーティションを保持するオプションが有効な場合でも、計算テーブルのパーティションに変更を適用する必要があります。
- 既存の AS Connection に対する [詳細プロパティ] ダイアログで、選択し直すまでリスト全体が表示されない問題を修正しました
- 一部のローカライズされたビルドで表示されたクリッピングされた UI 文字列の問題を修正しました
- 1400 互換性レベル AS 表形式モデルの PowerQuery 統合でのいくつかの問題を修正しました
- レポート ウィザード スタイル テンプレートが正しく表示されない問題を修正しました
- SQL から AS に変更するとデータ ソース設定が正しくなくなるレポート ウィザードの問題を修正しました
- コマンド ライン (devenv.com\exe) からの Analysis Services (表形式) プロジェクトのビルドが失敗する問題を修正しました
- := の前にある文字で始まる場合に強調表示された正しいテキストの色で表示されるように DAX メジャー パーサーの問題を修正しました
- 統合ワークスペース モードで表形式プロジェクトのすべてのファイルを表示しようとしてパスが長すぎる場合に ObjectRefException をトリガーする問題を修正しました
- Compact 4.0 Client Data Provider のデータ ソース デザイナーが使用できない問題を修正しました
- VS2017 で AS マイニング モデルを参照しようとしてエラーが発生した問題を修正しました
- VS2017 の AS 多次元モデルで、ビューの変更後に DSV ダイアグラムがレンダリングを停止して例外が検出される問題を修正しました
- VS2017 で AS 接続時のレポートのプレビューが失敗した問題を修正しました
 

**RS プロジェクト:**
- SSDT でレポートをデザインしているときに、大半を変更すると、パラメーターのツリー ビュー、データ ソース、およびデータセットが折りたたまれる問題を修正しました 
- 保存の操作で、最新バージョンではなく、RDL のバージョンが保存されるという問題が修正されました。
- バックアップが無効になっているときに SSDT RS がファイルをバックアップするという問題と他のいくつかの問題が修正されました。
- レポート ビルダーで [セルの分割] をクリックするとエラーが表示されるという問題が修正されました ( [Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/3101818/ssdt-2015-ssrs-designer-error-by-matrix-cell-split)を参照)。
- キャッシュが原因でレポートに誤ったデータが表示される場合があるという問題が修正されました ( [Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/3102158/ssdtbi-14-0-60812-report-preview-data-is-frequently-wrong-due-to-bad-caching)を参照)。

**IS プロジェクト:**
- run64bitruntime 設定が固定されないという問題が修正されました。
- DataViewer で表示されている列が保存されないという問題が修正されました。
- パッケージ パーツで注釈が非表示になるという問題が修正されました ( [Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/3106624/package-parts-hide-annotations)を参照)。
- パッケージ パーツでデータ フローのレイアウトと注釈が破棄されるという問題が修正されました ( [Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/3109241/package-parts-discard-data-flow-layouts-and-annotations)を参照)。
- SQL Server からのプロジェクトのインポート時に SSDT がクラッシュするという問題が修正されました。
- 保存されていた SSIS パッケージを開いた後の実行時に Hadoop ファイル システム タスクの TimeoutInMinutes が既定で 10 になる問題を修正しました。

**データベース プロジェクト:**
- SSDT DACPAC のデプロイで、IgnoreColumnOrder の追加設定が復活しました ([Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/1221587/ssdt-dacpac-deploy-add-setting-back-in-for-ignorecolumnorder)を参照)。
- STRING_SPLIT を使用した場合、SSDT でのコンパイルは失敗します ([Connect アイテム](https://connect.microsoft.com/SQLServer/feedback/details/2906200/ssdt-failing-to-compile-if-string-split-is-used)を参照)。
- DeploymentContributors でパブリック モデルにアクセスできるが、バッキング スキーマが初期化されていない問題を修正しました ([GitHub の問題](https://github.com/Microsoft/DACExtensions/issues/8)を参照)
- ファイル グループの配置に対する DacFx を一時的に修正しました。
- 外部シノニムに対する「未解決の参照」エラーを修正しました。 
- Always Encrypted:オンライン暗号化では、キャンセル時の変更追跡は無効にできず、暗号化を開始する前に変更追跡がクリーニングされていない場合は適切に機能しません。

## <a name="165nbsp-ssdt-for-vs-2015"></a>16.5、&nbsp;VS 2015 用 SSDT

_リリース済み:_ &nbsp; 2016 年 10 月 20 日  
_ビルド番号:_ &nbsp; 14.0.61021.0  
_Visual Studio 2015 用 SSDT。_  
_SQL Server 2016 までのサポート。_

**新機能**


### <a name="connection-improvements"></a>接続の強化

* **[参照]** タブの新しい検索ボックスを使用すると、ローカル サーバー、ネットワーク サーバー、および Azure SQL データベースをフィルター処理できます。 これは、多数のサーバーまたはデータベースがリストに表示される場合に便利です。
* **[履歴]** タブには、お気に入りをピン留めする、またはピン留めを外すための右クリック メニュー オプションと、履歴から接続を削除するための新しいオプションがあります。

### <a name="sqlpackage-and-dacfx-api-improvements"></a>SqlPackage および DacFx API の強化

SqlPackage.exe と DacFx API を使用すると、配置レポートと配置スクリプトの生成、およびデータベースへの発行を 1 回のアクションで実行できるようになりました。 これは、配置時に発行された内容のレポートを保持する場合に時間の節約になります。 もう 1 つのメリットとして、Azure のシナリオにおいて、マスター データベース用のスクリプトと配置ターゲット用のスクリプトが個別に作成されます。 これまでは 1 つのスクリプトが作成されており、配置を繰り返し行う際には役立ちませんでした。

SqlPackage の発行アクションとスクリプト アクションには、2 つの新しい引数が追加されました。

* DeployScriptPath (省略名: dsp): これは、配置スクリプトの書き込み先のパスです (省略可能)。 Azure の配置では、DB を作成または変更するための TSQL コマンドがある場合に、マスター スクリプトが同じパスに書き込まれますが、出力ファイル名として "Filename_Master.sql" が使用されます。
* DeployReportPath (省略名: drp): これは、配置レポートの書き込み先のパスです (省略可能)。

スクリプト アクションの場合は、既存の出力パス引数または新しいスクリプト/レポート固有の引数を使用する必要があります。ただし、両方を使用することはできません。

使用例:

**発行アクション**

```Sqlpackage.exe /a:Publish /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:"My\DeployScript.sql" /deployreportpath:"My\DeployReport.xml"```

**スクリプト アクション**

```Sqlpackage.exe /a:Script /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:"My\DeployScript.sql" /deployreportpath:"My\DeployReport.xml"```

DacFx に 2 つの新しい API、DacServices.Publish() と DacServices.Script() が追加されました。 これらは、発行 + スクリプト + レポートの各アクションを 1 回の操作で実行できるようサポートします。 使用例:

```
DacServices service = new DacServices(connectionString);
using(DacPackage package = DacPackage.Load(@"C:\My\db.dacpac")) {
var options = new PublishOptions() {
    GenerateDeploymentScript = true, // Should a deployment script be created?
    GenerateDeploymentReport = true, // Should an xml deploy report be created?
    DatabaseScriptPath = @"C:\My\OutputScript.sql", // optional path to save script to
    MasterDbScriptPath = @"C:\My\OutputScript_Master.sql", // optional path to save master script to
    DeployOptions = new DacDeployOptions()
};

// Call publish and receive deployment script & report in the results
PublishResult result = service.Publish(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);

// Call script and receive deployment script & report in results
result = service.Script(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);
```

**Analysis Services と Reporting Services**

SSAS 表形式デザイナーの DAX パーサーにおいて、大きな DAX 式を使用する際のパフォーマンスが向上しました。
詳しくは、[Analysis Services に関するブログ記事](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/)をご覧ください。

### <a name="fixed--improved-this-month"></a>今月の修正点/強化点

**データベース ツール**

* [接続のバグ 3055711](https://connect.microsoft.com/SQLServer/feedback/details/3055711/columns-cannot-be-selected-from-cross-apply-openjson-with-explicit-schema) - 明示的なスキーマを使用する CROSS APPLY OPENJSON から列を選択できません
* 修正 - 自動生成された履歴テーブルのインデックスに関する問題。再配置の際に DacFx がインデックスを削除します
* 修正 - DacFx のバッチ パーサーがエスケープした角かっこ "]" を解析しない問題。これにより、発行が失敗していました
* 強化 - SqlPackage のヘルプ出力に各アクションの説明が含まれるようになりました
* 修正 - [詳細設定] オプションの編集時、および発行、スキーマ比較、その他のファイルに保存された接続文字列の編集時に、接続ダイアログの [パスワードを記憶する] オプションが保持されていませんでした
* 修正 - [履歴] タブに表示される接続で IntegratedAuthentication=true の場合、接続プロパティの [認証] フィールドが空白のままになっていました。 現在は、想定どおり、[Windows 認証] と表示されます
* 修正 - [ツール] -> [オプション] -> [テキスト エディター] で、SQL Server Tools の Intellisense の設定に対する変更が保持されていませんでした
* 強化 - [履歴] タブの接続ダイアログにある [ピン留め]/[ピン留めを外す] ボタンがコンパクトになり、スクロール バーが表示される可能性が少なくなりました
* 修正 - 接続ダイアログのアクセシビリティに関するいくつかの問題が修正されました。

**Analysis Services と Reporting Services**

* SSDT AS のテーブル デザイナーにおいて、特定の状況でデータ グリッドのスクロール バーのつまみをクリックするとクラッシュしていた問題を修正しました。
* SSDT AS のテーブルで接続を現在のユーザーとして偽装するオプションを使用できない問題を修正しました
* SSDT AS のテーブル デザイナーにおいて、数式バーを大きく展開しすぎると、プロジェクトを再度開けなくなる問題を修正しました
* SSDT AS のテーブル デザイナーにおいて、テーブル タブが選択された場合にキーを押すとクラッシュが発生する問題を修正しました。
* SSDT AS のプロジェクトにおいて、[Excel で分析] から下位の AS サーバー バージョンに接続できない問題を修正しました。

**統合サービス**

* 接続のバグ  [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks) の修正:複数の統合サービス パッケージのタスクの移動

## <a name="164-ssdt-for-vs-2015"></a>16.4、VS 2015 用 SSDT

_リリース済み:_ &nbsp; 2016 年 9 月 20 日  
_ビルド番号:_ &nbsp; 14.0.60918  
_SQL Server 2016 の場合。_

**新機能**

SqlPackage.exe および Data-Tier Application Framework (DacFx) API でスキーマ比較がサポートされるようになりました。 詳しくは、「 [Schema Compare in SqlPackage and the Data-Tier Application Framework](https://blogs.msdn.microsoft.com/ssdt/2016/09/20/schema-compare-in-sqlpackage-and-the-data-tier-application-framework-dacfx/)」(SqlPackage および Data-Tier Application Framework におけるスキーマ比較) をご覧ください。

**Analysis Services - SSDT テーブル (SSAS) 統合のワークスペース モード**

SSDT テーブルに内部 SSAS インスタンスが含まれるようになりました。これにより、統合ワークスペース モードが有効な場合は、SSDT テーブルがバックグラウンドで自動的に起動するため、テーブル、列、データをモデル デザイナーで追加および表示できます。外部のワークスペース サーバー インスタンスを指定する必要はありません。 統合ワークスペース モードを使用しても、SSDT テーブルがワークスペース サーバーおよびデータベースと連動するしくみは変わりません。 変わるのは、SSDT テーブルがワークスペース データベースをホストする場所です。 統合ワークスペース モードを有効にするには、新しい表形式プロジェクトの作成時に表示される [テーブル モデル デザイナー] ダイアログ ボックスの [統合ワークスペース] オプションを選択します。 明示的なワークスペース サーバーを現在使用している既存の表形式プロジェクトの場合は、[プロパティ] ウィンドウで [統合ワークスペース モード] パラメーターを True に設定して統合ワークスペース モードに切り替えることができます。このパラメーターは、ソリューション エクスプローラーで Model.bim ファイルを選択すると表示されます。 詳しくは、[Analysis Services に関するブログ記事](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/)をご覧ください。

**データベース ツールの更新および修正点**
 **:**

- [接続の問題 3087775](https://connect.microsoft.com/SQLServer/feedback/details/3087775):VS データ ツールの 7 月の更新 14.0.60629.0 では、テンポラル テーブルが破損していました ("値を null にすることはできません。 パラメーター名: reportedElement")。
- [接続の問題 1026648](https://connect.microsoft.com/SQLServer/feedback/details/1026648):SSDT 比較では IsPersistedNullable が異なるものとして表示されます。
- [接続の問題 2054735](https://connect.microsoft.com/SQLServer/feedback/details/2054735):BACPAC のインポート時に ID がリセットされます。
- [接続の問題 2900167](https://connect.microsoft.com/SQLServer/feedback/details/2900167):SSDT 単体テストを実行すると一時ファイルが残ります。
- [接続の問題 1807712](https://connect.microsoft.com/SQLServer/feedback/details/1807712):下位互換性が確保されません - AppLocal と NuGet 化

**Analysis Services と Reporting Services**

* SSDT において、DirectQuery の計算列での DAX の編集時にエラーのヒントのポップアップが邪魔になる問題を修正しました。
* SSDT AS 表形式グリッドにおいて、Windows スケール ファクターが高 DPI (200% 以上) に設定されている場合に KPI アイコンがメジャー グリッドに表示されない問題を修正しました。
* SSDT AS において、大きなテーブル データを貼り付けると表形式プロジェクトが応答しなくなる問題を修正しました。
* SSDT AS のテーブル モデル エディターにおいて、接続フレンドリ名の変更時に、変更の保存が必要であるとモデルがマークされる問題を修正しました。
* SSDT AS の表形式プロジェクトにおいて、リレーションシップの管理ダイアログの列の幅を変更できない問題を修正しました。
* SSDT AS の 1200 レベルの表形式モデルにおいて、ドイツ語などのロケール設定を使用して Excel からデータを貼り付けると、コンマが小数点として正しく処理されない問題を修正しました。
* KPI アイコンが設定されている SSDT AS のプロジェクトにおいて、"このビジュアルのデータを取得できませんでした" というエラーが生成される問題を修正しました。
* 高 DPI スケールでサイズ変更する際に正しく固定される SSDT AS のプロジェクトのプロパティダイアログに関する問題を修正しました。
* SSDT AS のプロジェクトにおいて、貼り付けられたテーブルを含む特定のモデルのアップグレード中にエラーが発生する問題を修正しました。
* SSDT AS において、Excel からシート行全体を貼り付ける処理が遅く、不要な多数の列が作成される問題を修正しました。
* SSDT AS において、静的な大きい DataTable 式の解析と強調表示が遅い、または応答が停止する問題を修正しました。
* SSDT AS において、エディターで選択した現在のパースペクティブにメジャーと KPI 値を追加する際の問題を修正しました。
* SSDT において、SQL Azure から AS プロジェクトへのデータのインポートで "dbo" 以外のスキーマの種類がサポートされない問題を修正しました。

## <a name="163nbsp-ssdt-for-vs-2015"></a>16.3、&nbsp;VS 2015 用 SSDT

_リリース済み:_ &nbsp; 2016 年 8 月 15 日  
_ビルド番号:_ &nbsp; 14.0.60812.0  
_SQL Server 2016 の場合。_

**新機能**

- **リリース バージョン管理と番号付け:** 月別ではなく数値でリリースがタグ付けされるようになりました。 これは新しい SSMS ポリシーに準拠したもので、リリースや修正プログラムが 1 か月に複数ある場合の処理が簡略化されます。 このリリースは 16.3 であり、RTM リリース後の 3 回目の更新であることを意味します。 修正プログラムは 16.3.1 のように表記され、次回の更新 (来月を予定) は 16.4 になります。
- **Analysis Services - 表形式モデル エクスプローラー:** 表形式モデル エクスプローラーを使用すると、モデル内のさまざまなメタデータ オブジェクト (データ ソース、テーブル、メジャー、リレーションシップなど) 間を移動できます。 このエクスプローラーは個別のツール ウィンドウとして実装されます。Visual Studio の [表示] メニューを開いて [その他のウィンドウ] をポイントし、[表形式モデル エクスプローラー] をクリックすると表示できます。 既定では、表形式モデル エクスプローラーは個別のタブのソリューション エクスプローラー領域に表示されます。表形式モデル エクスプローラーでは、メタデータ オブジェクトが、表形式モデル 1200 のスキーマによく似たツリー構造で表示されます。また、多数の新機能も追加されています。
- **データベース ツール - Always Encrypted**:このリリースには、新しい [Always Encrypted キー管理](../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)ダイアログが用意されています。これにより、データベース プロジェクトまたは SQL Server オブジェクト エクスプローラーのライブ データベースに列マスター キーまたは列暗号化キーを簡単に追加できます。 このリリースは、Windows 証明書ストアの証明書をサポートしています。 今後のリリースでは、Azure Key Vault および CNG プロバイダーがサポートされる予定です。
    - 列マスター キーまたは列暗号化キーを作成する際、[データベースの更新] のクリック直後に SQL Server オブジェクト エクスプローラーに変更が反映されない可能性があります。 回避するには、SQL Server オブジェクト エクスプローラーでデータベース ノードを更新します。
    - SQL Server オブジェクト エクスプローラーからデータを含むテーブル内の列を暗号化しようとすると、エラーが発生する可能性があります。 現在、この機能は SSDT データベース プロジェクトと SSMS でのみサポートされています。 SQL Server オブジェクト エクスプローラーのサポートは今後のリリースで有効になる予定です。


**更新と修正点**
* **データベース ツール:**
    - **SSDT:**
        - 接続のバグ 1898001 [列の説明の 128 文字制限に関する問題を修正しました](https://connect.microsoft.com/SQLServer/feedback/details/1898001/column-description-limited-to-128-characters)。
        - VS からのデータベースの発行で発行プロファイル xml の DatabaseServiceObjective プロパティが適用されない問題を修正しました。
        - 接続のバグ 2900167 [単体テストの際に一時ファイルが正しく残らない問題を修正しました](https://connect.microsoft.com/SQLServer/feedback/details/2900167/running-ssdt-unit-tests-leaves-temp-files-behind)。
        - [データベースの設定] の [保有期間] コンボ ボックスが切り捨てられる問題を修正しました。
        - パスワードの変更時に、SQL CLR プロジェクトのプロパティで空の古いパスワードの検証が行われない問題を修正しました。
    - **DACFx:**
        - DACFx 互換性レベルが SqlAzureV12 エラーのために更新されない問題を修正しました。
        - IsAutoGeneratedHistoryTable プロパティがモデルの比較から正しく除外されない問題を修正しました。

- **Analysis Services と Reporting Services**
    - **SSDT:**
        - サーバー接続が失われると表形式モデルを保存できない問題を修正しました。
        - AS の無限ループの問題が原因で SSDT が応答しなくなる問題を修正しました。
        - 式のコミット方法に基づく動作の不一致の原因となる DAX 式の問題を修正しました。
        - KPI 作成時の VS のクラッシュの問題を修正しました。
        - SQL Server 2008 R2、2012、および 2014 用の無効なレポートが生成される問題を修正しました。
        - .dwpro プロジェクトの無限ループ エラーの原因となる階層順の問題を修正しました。
        - RDL のダウングレードの際に完全なリビルドが必要になり、ユーザーの混乱を招く RS RDL の問題を修正しました。
        - [クライアント ツールに非表示] が無効になる KPI の問題を修正しました。

## <a name="july-2016nbsp-ssdt-for-vs-2015"></a>2016 年 7 月、&nbsp;VS 2015 用 SSDT

_リリース済み:_ &nbsp; 2016 年 6 月 30 日  
_ビルド番号:_ &nbsp; 14.0.60629.0  
_SQL Server 2016 の場合。_

**新機能**  
- **Always Encrypted のサポート:** このリリースでは、Always Encrypted 列があるデータベースで、Always Encrypted がコア API とコマンド ライン ツール (SqlPackage.exe) を通じて完全にサポートされます。 Always Encrypted のすべての機能が完全にサポートされた状態でデータベース プロジェクトをビルドして発行できます。  
- **テンポラル テーブルのサポートの強化:** テンポラル テーブルのリンクを変更前に解除し、これらが完了したら再リンクするようにして、処理を簡略化しました。 つまり、サポートされる操作に関して、テンポラル テーブルが他の種類のテーブル (標準、メモリ内) と同等になります。 
- **SqlPackage.exe とインストールの変更:** SSDT を SQL Server エンジンと SSMS の更新から切り離すための変更を行いました。 詳しくは、「[Changes to SSDT and SqlPackage.exe installation and updates](https://blogs.msdn.microsoft.com/ssdt/2016/06/30/changes-to-ssdt-and-sqlpackage-exe-installation-and-updates/)」(SSDT と SqlPackage.exe のインストールおよび更新の変更) をご覧ください。

 

**更新と修正点**
* **データベース ツール:**
    * 今後、SSDT がデータベースで Transparent Data Encryption (TDE) を無効にすることはありません。 これまでは、プロジェクトのデータベース設定における既定の暗号化オプションが無効であると、暗号化がオフになっていました。 この修正により、暗号化を有効にすることができ、発行中に無効になることはありません。 
    * 初期接続時の Azure SQL DB 接続の再試行の回数が増えて、回復性が向上しました。
    * 既定のファイル グループが PRIMARY でない場合は、Azure V12 へのインポート/発行が失敗していました。 現在では、発行時にこの設定が無視されるようになりました。
    * 引用符で囲まれた識別子がオンになっているオブジェクトを含むデータベースのエクスポート時に、一部のインスタンスでエクスポートの検証が失敗する問題を修正しました。
    * Hekaton テーブルの作成用の TEXTIMAGE_ON オプションが許可されていない場合に正しく追加されない問題を修正しました。
    * データ フェーズの完了後の model.xml ファイルへの書き込みによってファイルの内容の書き換えが発生するため、大量のデータを使用したエクスポートに時間がかかる問題を修正しました。
    * Azure SQL DW および APS 接続用のセキュリティ フォルダーにユーザーが表示されない問題を修正しました。


 * **Analysis Services と Reporting Services:**
    * MSOLAP OLEDB プロバイダーに関する SxS の問題を修正しました。この場合、32 ビット プロバイダーだけがインストールされて、SQL Server 2014 に接続する 64 ビットの Excel 2016 に影響を及ぼします (Office365 からの ClickOnce のインストールでは再現せず、MSI Excel のインストールでのみ発生します)。
    * 貼り付けられたテーブルを含む AS モデルを 1103 から 1200 互換性レベルにアップグレードすると、"リレーションシップで無効な列 ID が使用されています" というエラーが発生し、コーナー ケースがより強固になる問題を修正しました。
    * SSDT-BI 2013 が同じコンピューター上にある場合の SxS の問題を修正しました。この場合、SSDT 2015 のアンインストール後に AS モデル内のデータをインポートできません (カートリッジ共有のレジストリ設定)。
    * AS エンジンへの接続が失われた場合 (SSDT を一晩中開いたままにしておく、AS サーバーをリサイクルする、または接続が一時的に失われるその他のケース) の問題/クラッシュに対処するための堅牢性が強化されました。 
    * マルチモニターを使用する場合に、VS ではなく別の画面でダイアログが開く問題を修正しました。 
    * AS モデルの貼り付けられたテーブルでの HTML テーブル (グリッド データ) からの貼り付けのサポートを修正/有効にしました。 
    * 空の貼り付けられたテーブルの 1200 へのアップグレードが失敗する (メジャー用のコンテナー テーブルとしてのみ使用されます) 問題を修正しました。 
    * 貼り付けられたテーブルを含む AS 表形式モデルの 1200 へのアップグレードに関する問題を修正しました。このアップグレードは、(1200 の貼り付けられたテーブルに使用する) 計算テーブルに関する AS エンジンの問題を回避し、アップグレード後に新しい計算テーブルでプロセスを実行するための処理です。 
    * 不完全な DAX 式を含む新しい AS 1200 モデルの計算テーブルの作成を取り消す際にクラッシュが発生する問題を修正しました。 
    * DB 名とテーブル名が同じ場合に、AS サーバーから SSDT AS プロジェクトに 1200 モデルをインポートする際の問題を修正しました。 
    * 1103 表形式モデルの KPI メジャーの編集に関する問題を修正しました。 
    * AS 1200 モデルのグリッドに KPI メジャーを貼り付ける際に、オブジェクト参照が設定されていないという例外が発生する問題を修正しました。 
    * 計算テーブル内の列を 1200 モデルのダイアグラム ビューから削除できない問題を修正しました。 
    * コード ビューで model.bim プロジェクト ファイルのプロパティを表示する際に発生するオブジェクト参照が設定されていないという例外を修正しました。 
    * 貼り付けされたテーブルを作成するために AS モデルのグリッドにデータを貼り付けると、コンマを小数点として使用する国際ロケールで正しくない値が生成される問題を修正しました。 
    * SSDT で 2008 RS プロジェクトを開き、そのプロジェクトをアップグレードしないよう選択する際の問題を修正しました。 
    * 1200 互換性レベル モデルの計算テーブルの UI において、列の種類の既定の書式設定を使用して UI から書式設定の種類の変更を許可する際の問題を修正しました。 
    

## <a name="june-2016nbsp-ssdt-for-vs-2015"></a>2016 年 6 月、&nbsp;VS 2015 用 SSDT

_リリース済み:_ &nbsp; 2016 年 6 月 1 日  
_ビルド番号:_ &nbsp; 14.0.60525.0  
_SQL Server 2016 の場合。_

SSDT の一般提供 (GA) がリリースされました。 2016 年 6 月の SSDT GA の更新では、SQL Server 2016 RTM の最新の更新プログラムのサポートとさまざまなバグ修正が追加されました。 詳しくは、「[SQL Server Data Tools GA update for June 2016](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/)」(2016 年 6 月の SQL Server Data Tools の GA 更新) をご覧ください。

## <a name="additional-resources"></a>その他のリソース
  
[SQL Server Data Tools &#40;SSDT&#41; のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)  
[以前のリリースの SQL Server Data Tools (SSDT と SSDT-BI)](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)  
[データベース エンジンの新機能](https://msdn.microsoft.com/library/bb510411.aspx)  
[Analysis Services の新機能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
[Integration Services の新機能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
