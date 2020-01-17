---
title: Microsoft Connector for Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca25b7425ce74cea820e295a6a99bc3a3c1e2817
ms.sourcegitcommit: a02727aab143541794e9cfe923770d019f323116
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2020
ms.locfileid: "75755854"
---
# <a name="microsoft-connector-for-teradata-preview"></a>Microsoft Connector for Teradata (プレビュー)
[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Microsoft Connector for Teradata を使用すると、SSIS パッケージ内の Teradata データベースとの間でデータをエクスポートしたり、データを読み込んだりできます。

この新しいコネクタでは、1MB 対応のテーブルを持つデータベースがサポートされます。

## <a name="version-support"></a>バージョンのサポート

Microsoft Connector for Teradata では、次の Microsoft SQL Server 製品がサポートされています。

- Microsoft SQL Server 2019
- Microsoft SQL Server Data Tools (SSDT)

Microsoft Connector for Teradata では、Teradata Parallel Transporter Application Programming Language Interface を利用し、Teradata データベースとの間でデータを読み込んだり、エクスポートしたりします。 次のバージョンがサポートされています。

- Teradata Parallel Transporter (Teradata PT) 16.10
- Teradata Parallel Transporter (Teradata PT) 16.20

次の Teradata データベース バージョンのデータ ソースがサポートされています。

- Teradata Database 16.20
- Teradata Database 16.10
- Teradata Database 15.10
- Teradata Database 15.00

Teradata Parallel Transporter Application プログラミング インターフェイス プログラマー ガイドの詳細については、[Teradata ドキュメント](https://docs.teradata.com/)を確認してください。

## <a name="installation"></a>インストール

### <a name="prerequisite"></a>前提条件

32 ビット コンピューターの場合、[Teradata Tools and Utilities - Windows Installation Package](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package) から次のドライバーをインストールします。

- Teradata ODBC ドライバー (32 ビット)
- Teradata PT API (32 ビット)

64 ビットコンピューターの場合、次のドライバーをインストールします。

- Teradata ODBC ドライバー (64 ビット)
- Teradata PT API (64 ビット)

Teradata データベースのコネクタをインストールするには、[Microsoft Connector for Teradata](https://www.microsoft.com/download/details.aspx?id=100599) の最新版からインストーラーをダウンロードし、実行します。 そのうえでインストール ウィザードの指示に従います。

コネクタをインストールしたら、SQL Server 統合サービスを再起動して、Teradata のソースと変換先が正常に機能することを確認する必要があります。

SQL Server 2017 以前をターゲットとする SSIS パッケージを実行するには、以下のリンクから対応するバージョンの **Microsoft Connector for Teradata by Attunity** をインストールする必要があります。

- [SQL Server 2017:Microsoft Connector Version 5.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016:Microsoft Connector Version 4.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014:Microsoft Connector Version 3.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012:Microsoft Connector Version 2.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="uninstallation"></a>アンインストール

アンインストール ウィザードを実行し、**Microsoft Connector for Teradata** を削除できます。

## <a name="next-steps"></a>次のステップ

- [Teradata 接続マネージャー](teradata-connection-manager.md)を構成する
- [Teradata ソース](teradata-source.md)を構成する
- [Teradata 変換先](teradata-destination.md)を構成する
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA6iwdw)を参照してください。
