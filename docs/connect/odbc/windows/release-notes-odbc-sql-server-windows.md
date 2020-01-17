---
title: Windows 上の SQL Server に対する ODBC のリリース ノート | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
ms.reviewer: v-jizho2, v-chojas, genemi
author: v-makouz
ms.author: v-makouz
manager: kenvh
ms.openlocfilehash: 98e7aec7883bc12d04ce24aba7b9a93244f707f6
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041157"
---
# <a name="release-notes-for-odbc-to-sql-server-on-windows"></a>Windows 上の SQL Server に対する ODBC のリリース ノート

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

このリリース ノート記事では、Windows 上の SQL Server に対する Microsoft ODBC ドライバーの新機能について説明します。

<!--
PLEASE USE THE STANDARD 2-COLUMN TABLE FORMAT!

For all our Release Notes articles (What's New too?), we are standardizing on the 2-column format that you see here for version "## 17.3".

Going forward, all new additions to this article must use the 2-column format.

Also, use the shorter ## H2 title format, which eliminates all the redundant constants, and appends the date-added.
One beneift of shortness is the avoidance of the annoying wrapping of unnecessarily long H2 titles in the rightNav.
- OLD H2:  ## What's New in the [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows
- NEW H2:  ## 17.3, February 2019

By the way, in GitHub, the file name is changing today 2019/03/30:
- FROM:  docs/connect/odbc/windows/release-notes.md
- TO  :  docs/connect/odbc/windows/release-notes-odbc-sql-server-windows.md

Thank you.
GeneMi (and CraigG).  2019/03/30.
-->

## <a name="1742-october-2019"></a>17.4.2、2019 年 10 月

| 追加された機能 | 詳細 |
| :------------ | :------ |
| 追加の Azure Key Vault エンドポイントのサポート | [ODBC ドライバーでの Always Encrypted の使用](../using-always-encrypted-with-the-odbc-driver.md)に関するページをご覧ください。 |
| データ分類バージョンの設定のサポート | 「[データ分類](../data-classification.md#bkmk-version)」を参照してください。 |
| Azure への認証に使用する Azure Active Drirectory Authentication Library (adal) がドライバーによってインストールされるようになりました | |
| バグの修正。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="174-july-2019"></a>17.4、2019 年 7 月

| 追加された機能 | 詳細 |
| :------------ | :------ |
| セキュリティで保護されたエンクレーブが設定された Always Encrypted。 | [ODBC ドライバーでの Always Encrypted の使用](../using-always-encrypted-with-the-odbc-driver.md)に関するページをご覧ください。 |
| 構成可能な TCP キープアライブ設定。 | 「[SQL Server への接続](../linux-mac/connection-string-keywords-and-data-source-names-dsns.md)」をご覧ください。 |
| バグの修正。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>17.3、2019 年 2 月

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Azure Active Directory マネージド サービス ID (システムおよびユーザー割り当て) 認証モード。 | 「[ODBC ドライバーでの Azure Active Directory の使用](../using-azure-active-directory.md)」を参照してください。 |
| Always Encrypted 列に対して入力パラメーターをストリーム配信する機能。 | 「[Limitations of the ODBC driver when using Always Encrypted (Always Encrypted を使用するときの ODBC ドライバーの制限事項)](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)」をご覧ください。 |
| XA 分散トランザクション。 | 「[Using XA Transactions (XA トランザクションの使用)](../use-xa-with-dtc.md)」をご覧ください。 |
| バグの修正。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2、2018 年 7 月

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Azure SQL Database と SQL Server のデータ分類。 | 「[データ分類](../data-classification.md)」をご覧ください。 |
| UTF-8 サーバー エンコードのサポート。 | &nbsp; |
| バグの修正。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1、2018 年 3 月

| 追加された機能 | 詳細 |
| :------------ | :------ |
| `SQL_COPT_SS_CEKCACHETTL` および `SQL_COPT_SS_TRUSTEDCMKPATHS` 接続属性のサポート。 | &bull; &nbsp; `SQL_COPT_SS_CEKCACHETTL`<br/>列暗号化キーのローカル キャッシュが存在する時間を制御したり、それをフラッシュしたりできます。<br/><br/>&bull; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`<br/>アプリケーションで、AE 操作が指定したリストの列マスター キーのみを使用するように制限できます。<br/><br/> 詳しくは、「[SQL Server 用 ODBC ドライバーと共に Always Encrypted を使用する](../using-always-encrypted-with-the-odbc-driver.md)」をご覧ください。 |
| Azure Active Directory 対話型認証のサポート | &nbsp; |
| バグの修正。 | 「[Bug fixes (バグの修正)](../bug-fixes.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

## <a name="17-february-2018"></a>17、2018 年 2 月

| 追加された機能 | 詳細 |
| :------------ | :------ |
| BCP API の Always Encrypted サポート。 | &nbsp; |
| 新しい接続文字列属性 `UseFMTOnly`。 | ドライバーは一時テーブルを必要とする特殊なケースで以前のメタデータを使用します。 |
| Azure SQL Managed Instance のサポート。 | プライベート プレビューの延長。<br/><br/>後の「[Managed Instance (ODBC バージョン 17) を使用するときの相違点](#diffs-managed-instance-17)」の一覧をご覧ください。 |
| &nbsp; | &nbsp; |

| 依存関係の変更 | 詳細 |
| :------------ | :------ |
| 削除された Microsoft オンライン サービス サインイン アシスタント | 依存関係が削除されました。 |
| &nbsp; | &nbsp; |

### <a name="diffs-managed-instance-17"></a> Managed Instance (ODBC バージョン 17) を使用するときの相違点

このバージョンの ODBC には、Azure SQL Managed Instance (延長されたプライベート プレビュー) のサポートが含まれます。 Managed Instance を使用するときは、以下で示す相違点の一覧をご覧ください。

> [!NOTE]
> Managed Instance を使用するときはいくつかの相違点があります。
>
> - FILESTREAM はサポートされていません。
> - ローカル ファイル システムのアクセスはサポートされていませんが、トレース ファイルなどの場合は必要です。
> - ローカル パスからの UDT の作成はサポートされていません。
> - Windows 統合認証はサポートされていません。
> - DTC はサポートされていません。
> - `sa` アカウントは存在しません (既定のアカウントは `cloudSA` と呼ばれます)。
> - TDS トークン エラー (0xAA) では、正しくないサーバー名が返されます。
> - データベース名の特殊文字はサポートされていません。
> - ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] はサポートされていません。
> - 言語設定に関係なく、エラー メッセージは常に英語で表示されます (Azure と同じ)。

## <a name="131"></a>13.1

| 追加された機能 | 詳細 |
| :------------ | :------ |
| ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、[Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) および [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) のサポートが追加されています。 | これらの追加されたサポートは、Microsoft SQL Server 2016 以降のバージョンに接続するときに使用できます。 |
| Always Encrypted および Azure Active Directory のサポートに対応する接続プールのキーワードと属性があります。 | これらのキーワードと属性については、「[Driver Aware Connection Pooling in the ODBC Driver for SQL Server (ODBC Driver for SQL Server でのドライバー対応接続プール)](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)」で説明されています。 |
| &nbsp; | &nbsp; |

## <a name="13"></a>13

| 追加された機能 | 詳細 |
| :------------ | :------ |
| Microsoft SQL Server 2016 のサポートが追加されます。 | ODBC ドライバー バージョン 11 の機能が保持されます。 |
| &nbsp; | &nbsp; |

## <a name="11"></a>11

| 追加された機能 | 詳細 |
| :------------ | :------ |
| 新しい機能が含まれます。 | 「[Microsoft ODBC Driver for SQL Server on Windows の機能](features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)」をご覧ください。 |
| SQL Server 2012 Native Client の ODBC に付属するすべての機能が含まれています。 | &nbsp; |
| &nbsp; | &nbsp; |
