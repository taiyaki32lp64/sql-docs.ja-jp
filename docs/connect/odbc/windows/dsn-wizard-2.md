---
title: データソースウィザード画面 2 (ODBC Driver for SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
ms.openlocfilehash: 4ab8be02351a23c78251a99ca707e946ee8944c8
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152568"
---
# <a name="data-source-wizard-screen-2"></a>データ ソース ウィザード画面 2

データ ソースの構成時に ODBC Driver for SQL Server で SQL Server への接続に使用される認証方法の指定、Microsoft SQL Server アドバンスト クライアント エントリのセットアップ、およびログインとパスワードの設定を行います。

## <a name="options"></a>オプション

### <a name="with-integrated-windows-authentication"></a>統合 Windows 認証を使う

ドライバーが SQL Server へのセキュリティで保護された (または信頼された) 接続を要求することを指定します。 オンにすると、SQL Server では、サーバーの現在のログイン セキュリティ モードに関係なく、統合ログイン セキュリティを使用して、このデータ ソースを使用する接続を確立します。 指定された任意のログイン ID またはパスワードは無視されます。 SQL Server システム管理者は、Windows ログインを SQL Server ログイン ID (たとえば、SQL Server Management Studio を使用) に関連付けている必要があります。

必要であれば、サーバーのサービス プリンシパル名 (SPN) を指定できます。

### <a name="with-active-directory-integrated-authentication"></a>Active Directory 統合認証を使用する

ドライバーが Azure Active Directory を使用して SQL Server に認証するように指定します。 オンにすると、SQL Server では、サーバーの現在のログイン セキュリティ モードに関係なく、Azure Active Directory 統合ログイン セキュリティを使用して、このデータ ソースを使用する接続を確立します。

### <a name="with-sql-server-authentication"></a>SQL Server 認証を使用する

ドライバーがログイン ID とパスワードを使用して SQL Server に認証するように指定します。

### <a name="with-active-directory-password-authentication"></a>Active Directory パスワード認証を使用する

ドライバーが Azure Active Directory のログイン ID とパスワードを使用して SQL Server に認証するように指定します。

### <a name="with-active-directory-interactive-authentication"></a>Active Directory 対話型認証を使用する

ログイン ID を指定することによって、ドライバーが Azure Active Directory 対話モードで SQL Server を認証するように指定します。 これにより、Azure 認証プロンプトダイアログがトリガーされます。

### <a name="login-id"></a>Login ID

ユーザーが入力した**ログイン id とパスワード**、または**ユーザーが入力したログイン id とパスワードを使用して Active Directory パスワード認証を使用して SQL Server 認証を使用している場合に、SQL Server に接続するときにドライバーが使用するログイン id を指定します。** または**Active Directory ユーザーが入力したログイン ID を使用した対話型認証**が選択されています。 これは、サーバーの既定の設定を確認するために確立された接続のみに適用されます。そのため、データ ソースが作成された後にそのデータ ソースを使用して確立された以降の接続には適用されません。

### <a name="password"></a>Password

ユーザーが入力した**ログイン id とパスワード**、または**ユーザーが入力したログイン id とパスワードを使用して Active Directory パスワード認証を使用して SQL Server 認証を使用している場合に、SQL Server に接続するときにドライバーが使用するパスワードを指定します。** が選択されています。 これは、サーバーの既定の設定を確認するために確立された接続のみに適用されます。そのため、新しいデータ ソースを使用して確立された以降の接続には適用されません。

**[ログイン ID]** ボックスと **[パスワード]** ボックスは、 **[統合 Windows 認証]** または **[Active Directory 統合認証]** を使用 が選択されている場合は無効になります。

### <a name="next"></a>Next

ウィザードの次の画面に進みます。

### <a name="back"></a>戻る

ウィザードの前の画面に戻ります。

## <a name="next-steps"></a>次の手順

[データ ソース ウィザード画面 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[データ ソース ウィザード画面 3](../../../connect/odbc/windows/dsn-wizard-3.md)

