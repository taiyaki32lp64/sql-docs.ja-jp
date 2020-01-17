---
title: SQL Server Data Tools (SSDT) での Azure Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 302345a2d7e8c1bd9192c91c6f88253c9a4668f2
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049904"
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) での Azure Active Directory のサポート

[!INCLUDE[appliesto-xx-asdb-asdb-xxx-md.md](../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

SQL Server Data Tools (SSDT) では、[Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) の認証方法がいくつか用意されています。

Visual Studio で **[SQL Server オブジェクト エクスプローラー]** ( **[表示]** メニュー) を開き、 **[SQL Server の追加]** を選択します。

![SSDT 接続ダイアログ](media/azure-active-directory/interactive.png)

#### <a name="which-azure-sql-products"></a>対象となる Azure SQL 製品

この記事では、[Azure クラウド](https://azure.microsoft.com/)の次の *Azure SQL 製品*を対象に Azure AD について説明します。

- Azure SQL データベース
- Azure SQL Data Warehouse

## <a name="active-directory-password-authentication"></a>Active Directory パスワード認証

*Active Directory パスワード認証*は、上記の Azure SQL 製品に接続するメカニズムです。 このメカニズムでは、Azure Active Directory (Azure AD) の ID が利用されます。 次の状況で、この手法が接続に利用されます。

- Azure とフェデレーションしていないドメインから資格情報を利用して Windows にログインしている。
- Azure AD 認証と Azure AD を利用している。その基盤は初期またはクライアント ドメインである。

詳細については、「 [Azure Active Directory 認証を使用して SQL Database に接続する](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)」を参照してください。  

## <a name="active-directory-integrated-authentication"></a>Active Directory 統合認証

*Active Directory 統合認証*は、Azure Active Directory (Azure AD) の ID を使用して上記の Azure SQL 製品に接続するメカニズムです。 フェデレーション ドメインから Azure Active Directory の資格情報を使用して Windows にログインしている場合は、この方法を使用して接続します。 詳細については、「 [Azure Active Directory 認証を使用して SQL Database に接続する](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)」を参照してください。

## <a name="active-directory-interactive-authentication"></a>Active Directory 対話型認証

*Active Directory 対話型認証*は、SSDT を含む上記 Azure SQL 製品に接続するときに利用できますが、[.NET Framework 4.7.2](https://docs.microsoft.com/dotnet/api/?view=netframework-4.7.2) 以降のバージョンが必要になります。

- [各種バージョンの .NET Framework をダウンロードし、インストールする](https://www.microsoft.com/net/download/all)。
- [Visual Studio 2017 バージョン 15.6](https://docs.microsoft.com/visualstudio/releasenotes/vs2017-relnotes) またはそれ以降のバージョン。

#### <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)

Active Directory 対話型認証では、Azure Active Directory (AD) Multi-Factor Authentication (MFA) を使用して上記 Azure SQL 製品で認証することが可能な、対話型の認証がサポートされます。 この方法では、フェデレーションされたネイティブ Azure AD ユーザーと他のアカウントからのゲスト ユーザーを利用できます。 その他の種類のアカウント:

- 企業間取引 (Azure AD B2B) ユーザー。
- @outlook.com、@hotmail.com、@live.com など、Microsoft アカウント。
- @gmail.com など、Microsoft 以外のアカウント。

MFA 方法を指定すると、 **[ユーザー名]** を指定する必要があり、 **[パスワード]** フィールドが無効になります。 

#### <a name="password-entry"></a>パスワードの入力

*Active Directory 対話型認証*で認証する場合、ユーザーが手動でパスワードを入力する必要がある認証ウィンドウが開きます。

![サインイン ダイアログ](media/azure-active-directory/sign-in.png)

MFA の実施は、Azure AD によって、この追加の MFA ポップアップ ウィンドウを通じて提供されます。

> [!NOTE]
> *Active Directory 対話型認証*を使用すると、自動化されているワークフローがブロックされることがあります。 人が認証プロセスを操作し、手動でパスワードを入力する必要があります。

## <a name="known-issues-and-limitations"></a>既知の問題と制限事項

- *Active Directory 対話型認証*は、この記事の冒頭に記載している Azure SQL 製品に接続するときにのみ利用できます。 SQL Server (オンプレミスまたは VM 上) に対しては、この認証はサポートされていません。
- *Active Directory 対話型認証*は、*サーバー エクスプローラー*の接続ダイアログではサポートされません。 *SQL Server オブジェクト エクスプローラー*で SSDT を使用して接続する必要があります。
- 現在ログインしている Visual Studio アカウントとのシングル サインオン統合は、SSDT ではサポートされません。
- Visual Studio のインストール中に Extensions ディレクトリにインストールされる SQLPackage.exe は、その場所から使用するためのものではありません。 Azure AD で SQLPackage.exe を使用するには、[https://www.microsoft.com/download/details.aspx?id=55088](https://www.microsoft.com/download/details.aspx?id=55088) を参照してください 
- SSDT データ比較は、Azure AD 認証ではサポートされていません。  


## <a name="see-also"></a>参照  

[多要素認証](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)  
[SQL Database での Azure Active Directory 認証](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)  
[SSDT MSDN フォーラム](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT チーム ブログ](https://blogs.msdn.com/b/ssdt/)  
[DACFx API リファレンス](https://msdn.microsoft.com/library/dn645454.aspx)  
[SQL Server Management Studio (SSMS) のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)  
