---
title: Microsoft SQL Server 用 Drivers for PHP のリリース ノート | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-dapugl, kenvh
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ac53a8515f55dfc0cad282fd14294e5f285af9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935916"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft SQL Server 用 Drivers for PHP のリリース ノート

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このページでは、の各バージョンで追加さ[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]れた内容について説明します。  

<!--
Hello, We are standardizing the format of content inside our Release Notes (or What's New) articles.
Instead of bullets (or paragraphs), we have shifted to the 2-column format you see for H2 **What's New in Version 5.6**.
It is not necessary to reformat all the older H2 sections in this Release Notes file, but.....

Going forward, please be sure to use the 2-column format.

Also, all Release Notes .md file names now must begin with 'release-notes-*.md'.  And no filler words.
The 5.6 edition of this file is being renamed.....
FROM:  'release-notes-for-the-php-sql-driver.md'
TO  :  'release-notes-php-sql-driver.md'

For any questions, ask GeneMi or CraigG.
Thanks a lot.  2019-03-28  (DevO= 1467988)
-->

## <a name="whats-new-in-version-56"></a>バージョン 5.6 の新機能

| 新しい項目 | 詳細 |
| :------- | :------ |
| PHP 7.3 のサポート。 | &nbsp; |
| PHP 7.0 のサポートが削除されました。 | &nbsp; |
| すべてのプラットフォームで Microsoft ODBC Driver 17.3 がサポートされます。 | &nbsp; |
| MacOS Mojave のサポート。 | ODBC ドライバー17.3 以降が必要です。 |
| Ubuntu 18.10 および Suse Linux 15 のサポート。 | どちらにも ODBC Driver 17.3 以降が必要です。 |
| Linux Ubuntu 17.10 および macOS El Capitan のサポートが削除されました。 | &nbsp; |
| Azure AD アクセストークンのサポート。 | Linux および macOS では、ODBC Driver 17.2 + と unixODBC 2.3.6 + が必要です。 |
| Azure リソースの管理対象 Id を使用した Azure AD での認証のサポート。 | ODBC Driver 17.3 + が必要です。 |
| 新しいフェッチ機能 | &bull;&nbsp; Pdo_sqlsrv がオブジェクトとして DATETIME を返すための新しい PDO:: SQLSRV_ATTR_FETCHES_DATETIME_TYPE フラグ。<br/><br/>&bull;&nbsp; Sqlsrv のステートメントレベルに return? asstrings オプションを追加します。<br/><br/>&bull;&nbsp;フェッチされた結果の10進数値を書式設定するための両方のドライバーの接続レベルとステートメントレベルの新しいオプション。 |
| ユーザーがソースからのビルドを選択した場合の、ドライバーの静的コンパイルのサポート。 | &nbsp; |
| フェッチ時にメタデータをキャッシュし、Unicode 文字列変換を高速化することで、パフォーマンスが向上しました。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="whats-new-in-version-53"></a>バージョン 5.3 の新機能

- すべてのプラットフォームでの Microsoft ODBC Driver 17.2 のサポート
- MacOS High シエラレオネのサポート (ODBC Driver 17 以降が必要)
- Always Encrypted 機能が、[の PHP ドライバーで Always Encrypted を使用して](../../connect/php/using-always-encrypted-php-drivers.md)、サポートされているすべての Windows、Linux、または macOS プラットフォームで使用できるようにする、基本的な CRUD 機能の Always Encrypted の Azure Key Vault のサポート SQL Server
- Ubuntu 18.04 LTS のサポート (ODBC Driver 17.2 が必要)
- Linux または macOS での接続の回復性もサポートされる (ODBC Driver 17.2 が必要)

## <a name="whats-new-in-version-52"></a>バージョン 5.2 の新機能

- PHP 7.2.1 と Windows でのサポート、および他のプラットフォームでの7.2.0
- Microsoft ODBC Driver 17 のサポート
  - すべてのプラットフォームでバージョン17が既定になりました
- Ubuntu 17.10、Debian 9、Suse Enterprise Linux 12 のサポート
- Ubuntu 15.10 のサポートが削除されました
- Windows での CRUD 機能を使用した Always Encrypted のサポート。 詳しくは、「[SQL Server 用 PHP ドライバーと共に Always Encrypted を使用する](../../connect/php/using-always-encrypted-php-drivers.md)」をご覧ください
  - Windows 証明書ストアのサポート
  - Always Encrypted は、Microsoft ODBC Driver 17 以降でのみサポートされています。
- Linux と macOS での UTF8 以外のロケールのサポート
  - Linux および macOS の UTF8 以外のロケールは、Microsoft ODBC Driver 17 以降でのみサポートされています。
- Azure SQL Data Warehouse のサポート
- Azure SQL Managed Instance (延長されたプライベート プレビュー) のサポート

## <a name="whats-new-in-version-43"></a>バージョン 4.3 の新機能

- PHP 7.1 のサポート
- macOS Sierra および macOS El Capitan のサポート
- Ubuntu 15.10、Debian 8 のサポート
- Ubuntu 15.04 のサポートが削除されました
- 透過的なネットワーク IP 解決による Always On 可用性グループのサポート。 詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。
- 制限付きの sql_variant データ型のサポートを追加しました。
- Windows でのアイドル状態の接続の回復性のサポート。 詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。
- Linux と macOS の接続プールのサポート。 詳細については、[接続プール](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)に関するページを参照してください。
- ActiveDirectoryPassword と SqlPassword を使用した Azure Active Directory 認証のサポート。 詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。

## <a name="whats-new-in-version-40"></a>バージョン 4.0 の新機能

- PHP 7.0 のサポート  
- 完全な64ビットサポート
- Ubuntu 15.04、Ubuntu 16.04、および RedHat 7 のサポート

## <a name="whats-new-in-version-32"></a>バージョン 3.2 の新機能

- PHP 5.6 のサポート   
- 旧バージョンの PHP 5.5 および 5.4 最新の更新プログラムが含まれています   
- Microsoft SQL Server 用 ODBC Driver 11 が必要です  

## <a name="whats-new-in-version-31"></a>バージョン 3.1 の新機能

- PHP 5.5 のサポート  
- Microsoft SQL Server 用 ODBC Driver 11 が必要です。 以前のバージョンでは、SQL Native Client が必要でした。  

## <a name="whats-new-in-version-30"></a>バージョン 3.0 の新機能  

- PHP 5.4 のサポート  [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 3 では、PHP 5.2 はサポートされていません。  
- AttachDBFileName 接続オプションが追加されています。 詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。  
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で追加された LocalDB のサポート。 詳細については、「 [LocalDB のサポート](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)」を参照してください。
- AttachDBFileName 接続オプションが追加されています。 詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。  
- 高可用性のディザスター リカバリー機能のサポート。 詳細については、「[高可用性、障害復旧のサポート](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)」をご覧ください。
- クライアント側のカーソル (結果セットのメモリ内キャッシュ) のサポート。 詳細については、「[カーソルの種類 &#40;SQLSRV ドライバー&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)」および「[カーソルの種類 &#40;PDO_SQLSRV ドライバー&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)」を参照してください。
- PDO::ATTR_EMULATE_PREPARES 属性が追加されました。 詳細については、「[PDO::prepare](../../connect/php/pdo-prepare.md)」をご覧ください。  

## <a name="whats-new-in-version-20"></a>バージョン 2.0 の新機能

バージョン 2.0 では、PDO_SQLSRV ドライバーのサポートが追加されました。 詳細については、「 [PDO_SQLSRV ドライバー リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)」を参照してください。  

## <a name="see-also"></a>参照

[Microsoft SQL Server 用 Drivers for PHP の概要](../../connect/php/overview-of-the-php-sql-driver.md)
