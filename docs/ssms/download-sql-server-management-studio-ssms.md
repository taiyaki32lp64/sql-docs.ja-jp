---
title: SQL Server Management Studio (SSMS) のダウンロード | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein, maghan
ms.technology: ssms
ms.topic: conceptual
keywords:
- ssms のインストール、ssms のダウンロード、最新の ssms
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- sql management studio インストール
- ダウンロード sql management studio
- ms sql management studio
- install sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dnethi
ms.author: dinethi
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: 38c594e235bf68c18ec493fd8ec43f585ea0378c
ms.sourcegitcommit: 0c40843c13f67ba7d975f4fedb9d20d70747f66d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2019
ms.locfileid: "74097863"
---
# <a name="download-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) のダウンロード

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Management Studio (SSMS) は、SQL Server から Azure SQL Database まで、SQL インフラストラクチャを管理するための統合環境です。 SSMS には、SQL Server とデータベースのインスタンスを構成、監視、および管理するためのツールが備わっています。 SSMS を使用して、ご利用のアプリケーションで使われるデータ層コンポーネントを配置、監視、アップグレードしたり、クエリとスクリプトを作成したりすることができます。

SSMS を使用すると、データベースとデータ ウェアハウスがローカル コンピューターやクラウドなど、どこにあっても、クエリ、設計、および管理ができます。

SSMS は無料です。

## <a name="download-ssms"></a>SSMS のダウンロード

**[![ダウンロード](media/download-icon.png) SQL Server Management Studio (SSMS) のダウンロード](https://aka.ms/ssmsfullsetup)**

SSMS 18.4 は SSMS の GA (一般提供) 最新版です。 以前の GA バージョンの SSMS 18 がインストールされている場合、SSMS 18.4 をインストールすると、18.4 にアップグレードされます。 以前の "*プレビュー*" 版の SSMS 18.x がインストールされている場合は、それをアンインストールしてから SSMS 18.4 をインストールしてください。

### <a name="version-information"></a>バージョン情報

- リリース番号:18.4  
- ビルド番号:15.0.18206.0  
- リリース日:2019 年 11 月 4 日  

コメントや提案がある場合、または問題を報告する場合、SSMS チームに連絡する最適な方法は [UserVoice](https://aka.ms/sqlfeedback) です。

SSMS 18.x のインストールでは、17.x 以前のバージョンの SSMS がアップグレードまたは置き換えられることはありません。 SSMS 18.x は以前のバージョンとは別にサイド バイ サイドでインストールされるので、両方のバージョンを使用できます。

コンピューターに SSMS のサイド バイ サイドのインストールが含まれている場合は、特定のニーズに応じて適切なバージョンを起動してください。 最新バージョンには、**Microsoft SQL Server Management Studio 18** というラベルが付いています。

> [!Note]
> 英語以外のバージョンからこのページにアクセスしていて、最新の内容を見たい場合は、[サイトの英語 (米国) 版](https://aka.ms/downloadssmsusenglish)をご覧ください。 [使用できる言語](#available-languages)を選択して、英語 (米国) 版のサイトから別の言語をダウンロードできます。ます。

## <a name="available-languages"></a>使用できる言語

SSMS の今回のリリースは、次の言語でインストールできます。

SQL Server Management Studio 18.4:  
[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x40a)

> [!NOTE]
> SQL Server PowerShell モジュールは、PowerShell ギャラリーで入手できる独立したインストールです。 詳細については、「[SQL Server PowerShell モジュールのダウンロード](download-sql-server-ps-module.md)」を参照してください。

## <a name="new-in-this-release-ssms-184"></a>このリリースの新機能 (SSMS 18.4)

| [新しい項目] | 詳細 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| データ分類 | データ分類に対してカスタム情報保護ポリシーのサポートが追加されました。 |
| クエリ ストア | ダイアログのプロパティに "*クエリごとに最大プラン*" の値が追加されました。 |
| クエリ ストア | 新しいカスタム キャプチャ ポリシーのサポートが追加されました。 |
| SMO/スクリプト作成 | SQL DW で具体化されたビューのスクリプトをサポートします。 |
| SMO/スクリプト作成 | *SQL On Demand* のサポートが追加されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - 50 個の評価規則が追加されました (GitHub の詳細を参照)。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - ルールの条件に基になる計算式と比較が追加されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - RegisteredServer オブジェクトのサポートが追加されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - JSON 形式での規則の格納方法が更新され、オーバーライド/カスタマイズを適用するメカニズムも更新されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - Linux で SQL をサポートするための規則が更新されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - 規則セットの JSON 形式が更新され、SCHEMA バージョンが追加されました。 |
| SMO/スクリプト作成 | [SQL Assessment API](../sql-assessment-api/sql-assessment-api-overview.md) - 推奨事項の読みやすさが向上するように、コマンドレットの出力が更新されました。 |
| XEvent プロファイラー | XEvent プロファイラー セッションに *error_reported* イベントが追加されました。 |

このリリースの新機能の詳細については、[SSMS のリリース ノート](release-notes-ssms.md)に関するページをご覧ください。

## <a name="supported-sql-offerings-ssms-184"></a>サポートされる SQL 製品 (SSMS 18.4)

- このバージョンの SSMS は、すべての[サポート対象バージョンである SQL Server 2008 から [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) で動作し、Azure SQL Database および Azure SQL Data Warehouse で最新のクラウド機能と連携するための最大レベルのサポートを提供します。
- また、SSMS 18.x は、SSMS 17.x、SSMS 16.x または SQL Server 2014 SSMS 以前とサイドバイサイドでインストールできます。
- SQL Server Integration Services (SSIS) - SSMS バージョン 17.x 以降では、レガシ SQL Server Integration Services サービスへの接続はサポートされません。 以前のバージョンのレガシ Integration Services に接続するには、SQL Server のバージョンに対応する SSMS のバージョンを使用します。 たとえば、レガシ SQL Server 2016 Integration Services サービスに接続する場合は、SSMS 16.x を使用します。 SSMS 17.x および SSMS 16.x は、同じコンピューターにサイドバイサイドでインストールすることができます。 SQL Server 2012 のリリース以降では、SSIS カタログ データベースである SSISDB を使用して、Integration Services パッケージの格納、管理、実行、監視を行うことをお勧めします。 詳細については、「[SSIS カタログ](../integration-services/catalog/ssis-catalog.md)」をご覧ください。

## <a name="supported-operating-systems-ssms-184"></a>サポートされるオペレーティング システム (SSMS 18.4)

SSMS の今回のリリースでは、最新の Service Pack を使用した次の 64 ビット プラットフォームがサポートされます。

- Windows 10 (64 ビット) <sup>*</sup>
- Windows 8.1 (64 ビット)
- Windows Server 2019 (64 ビット)
- Windows Server 2016 (64 ビット) <sup>*</sup>
- Windows Server 2012 R2 (64 ビット)
- Windows Server 2012 (64 ビット)
- Windows Server 2008 R2 (64 ビット)

<sup>*</sup> バージョン 1607 (10.0.14393) 以降が必要

> [!NOTE]
> SSMS は Windows 上でのみ実行されます。 Windows 以外のプラットフォーム上で実行されるツールが必要な場合は、Azure Data Studio をご覧ください。 Azure Data Studio は、macOS、Linux、さらに Windows 上で実行される新しいクロスプラットフォーム ツールです。 詳しくは、[Azure Data Studio](../azure-data-studio/what-is.md) に関する記事をご覧ください。

## <a name="release-notes-ssms-184"></a>リリース ノート (SSMS 18.4)

このリリースには、[既知の問題](release-notes-ssms.md#known-issues-184)がいくつかあります。

このリリースの詳細については、[SSMS のリリース ノート](release-notes-ssms.md)に関するページをご覧ください。

## <a name="previous-ssms-releases"></a>以前のリリースの SSMS

[SQL Server Management Studio の以前のリリース](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>参照

- [チュートリアル: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio のドキュメント](sql-server-management-studio-ssms.md)
- [追加の更新プログラムとサービス パック](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [SQL Server Data Tools (SSDT) のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
