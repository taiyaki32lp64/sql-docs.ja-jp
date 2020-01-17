---
title: Microsoft Drivers for PHP for SQL Server のサポート マトリックス |Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: genemi
manager: ''
ms.openlocfilehash: 0790d2cc0497ef2912f96cd4679e4541fc9b2262
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63180274"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Microsoft PHP Drivers for SQL Server のサポート マトリックス

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このページには、Microsoft SQL Server 用 PHP Driver のサポート表とサポート ライフサイクル ポリシーがあります。

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP ドライバーのサポート ライフ サイクルの表とポリシー

マイクロソフト サポート ライフサイクル (MSL) ポリシーでは、マイクロソフト製品のサポート ライフサイクルを理解しやすくする、予測可能な情報を提供しています。 PHP ドライバーのバージョン 3.x、4.x、5.x には、ドライバーのリリース日から 5 年間のメインストリーム サポートが含まれています。 メインストリーム サポートについては、[マイクロソフト サポート ライフサイクルの Web サイト](https://support.microsoft.com/lifecycle)で定義されています。

延長サポートとカスタム サポートのオプションは、Microsoft PHP Driver では使用できません。

次の Microsoft PHP Driver は、表示されているサポートの終了日までサポートされます。

|ドライバー名|ドライバー パッケージのバージョン|メインストリーム サポートの終了|
|-|:-:|-|
|SQL Server 用 Microsoft PHP ドライバー 5.6|5.6|2024 年 2 月 21日|
|SQL Server 用 Microsoft PHP ドライバー 5.3|5.3|2023 年 7 月 20 日|
|SQL Server 用 Microsoft PHP ドライバー 5.2|5.2|2023 年 2 月 9 日|
|SQL Server 用 Microsoft PHP ドライバー 4.3|4.3|2022 年 7 月 6 日|
|SQL Server 用 Microsoft PHP ドライバー 4.0|4.0|2021 年 7 月 11 日|
|SQL Server 用 Microsoft PHP ドライバー 3.2|3.2|2020 年 3 月 9日に|
|SQL Server 用 Microsoft PHP ドライバー 3.1|3.1|2019 年 12 月 12日|
| &nbsp; | &nbsp; | &nbsp; |

次の Microsoft PHP ドライバーはサポートされなくなりました。

|ドライバー名|ドライバー パッケージのバージョン|メインストリーム サポートの終了|
|-|:-:|-|
|SQL Server 用 Microsoft PHP ドライバー 3.0|3.0|2017 年 3 月 6 日|
|SQL Server 用 Microsoft PHP ドライバー 2.0|2.0|2015 年 8 月 10 日|
|SQL Server 用 Microsoft PHP ドライバー 1.0|1.0|2014 年 4 月 28 日|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>SQL Server のバージョンの互換性を認定
 次の表は、テストして、対応するバージョンのドライバーと互換性のあるものとして認定されている SQL Server のバージョンを一覧表示します。 以前のバージョンのドライバーとの下位互換性を維持するために努力しますが、最新サポートされているドライバーのみをテストして、SQL Server がリリースされると、新しい SQL Server のバージョンを認定します。

|SQL Server ドライバーのバージョンの PHP&#8594;<br />&#8595; SQL Server のバージョン|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL Managed Instance<br/> (延長されたプライベート プレビュー)|Y|Y|Y|Y| | | | | |
|Azure SQL Data Warehouse|Y|Y|Y|Y| | | | | |
|SQL Server 2017         |Y|Y|Y|Y| | | | | |
|SQL Server 2016         |Y|Y|Y|Y|Y| | | | |
|SQL Server 2014         |Y|Y|Y|Y|Y|Y|Y| | |
|SQL Server 2012         |Y|Y|Y|Y|Y|Y|Y|Y| |
|SQL Server 2008 R2      |Y|Y|Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008         | | | | |Y|Y|Y|Y|Y|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="php-version-support"></a>PHP バージョンのサポート

Microsoft PHP ドライバーの一覧表示されているバージョンでは、次のバージョンの PHP がサポートされています。

|SQL Server ドライバーのバージョンの PHP&#8594;<br />&#8595; PHP バージョン|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|:---:|---|---|---|---|---|---|---|---|---|
|7.3|7.3.0+          |                |                |       |       | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |       | | | | |
|7.1|7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |       |        |        |        |        |
|7.0|                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|                |                |                |       |       |5.6.4+  |        |        |        |
|5.5|                |                |                |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|                |                |                |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|                |                |                |       |       |        |        |5.3.0   |5.3.0   |
|5.2|                |                |                |       |       |        |        |        |5.2.4<br />5.2.13|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. 7\.2.1 のバージョン、Windows でバージョン 7.2.0 中に後でサポートされ、後で、Linux と macOS でサポートされます。

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

Microsoft PHP ドライバーの一覧表示されているバージョンでは、次の Windows オペレーティング システムのバージョンがサポートされています。

|SQL Server ドライバーのバージョンの PHP&#8594;<br />&#8595; オペレーティング システム|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |Y  |Y  |Y  |Y  |   |   |   |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2008 R2 SP1          |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |   |Y  |
|Windows Server 2008 SP2             |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008                 |   |   |   |   |   |   |   |   |Y  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |   |   |Y  |
|Windows 10                          |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows 8                           |   |   |   |Y  |Y  |Y  |Y  |   |   |
|Windows 7 SP1                       |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Vista SP2                   |   |   |   |   |Y  |Y  |Y  |Y  |Y  |
|Windows XP SP3                      |   |   |   |   |   |   |   |   |Y  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

Microsoft PHP ドライバーの一覧表示されているバージョンでは、次の Linux と Mac のオペレーティング システムのバージョン (64 ビットのみ) がサポートされています。

|SQL Server ドライバーのバージョンの PHP&#8594;<br />&#8595; オペレーティング システム|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 18.10 (64 ビット)               |Y  |   |   |   |   |   |   |   |   |
|Ubuntu 18.04 (64 ビット)               |Y  |Y  |   |   |   |   |   |   |   |
|Ubuntu 17.10 (64 ビット)               |   |Y  |Y  |   |   |   |   |   |   |
|Ubuntu 16.04 (64 ビット)               |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Ubuntu 15.10 (64 ビット)               |   |   |   |Y  |   |   |   |   |   |
|Ubuntu 15.04 (64 ビット)               |   |   |   |   |Y  |   |   |   |   |
|Debian 9 (64 ビット)                   |Y  |Y  |Y  |   |   |   |   |   |   |
|Debian 8 (64 ビット)                   |Y  |Y  |Y  |Y  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 ビット) |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Suse Enterprise Linux 15 (64 ビット)   |Y  |   |   |   |   |   |   |   |   |
|Suse Enterprise Linux (64 ビット) の 12   |Y  |Y  |Y  |   |   |   |   |   |   |
|macOS Mojave (64 ビット)               |Y  |   |   |   |   |   |   |   |   |
|macOS High Sierra (64 ビット)          |Y  |Y  |   |   |   |   |   |   |   |
|macOS Sierra (64 ビット)               |Y  |Y  |Y  |Y  |   |   |   |   |   |
|macOS El Capitan (64 ビット)           |   |Y  |Y  |Y  |   |   |   |   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="see-also"></a>参照

[リリース ノート](../../connect/php/release-notes-php-sql-driver.md)

[サポート リソース](../../connect/php/support-resources-for-the-php-sql-driver.md)

[システム要件](../../connect/php/system-requirements-for-the-php-sql-driver.md)
