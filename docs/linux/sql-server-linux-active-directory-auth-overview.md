---
title: SQL Server on Linux に対する Active Directory 認証
titleSuffix: SQL Server
description: この記事では、SQL Server on Linux に対する Active Directory 認証の概要を説明します。
ms.date: 04/01/2019
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 32ff23fe1ea7f0a892a19cc6be0eef8439ee907f
ms.sourcegitcommit: 365a919e3f0b0c14440522e950b57a109c00a249
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75831824"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>SQL Server on Linux に対する Active Directory 認証

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux に対する Active Directory (AD) 認証の概要について説明します。 AD 認証は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では統合認証とも呼ばれます。

## <a name="ad-authentication-overview"></a>AD 認証の概要

AD 認証を使用すると、Windows または Linux 上のドメインに参加しているクライアントは、ドメインの資格情報と Kerberos プロトコルを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の認証を受けることができます。

AD 認証には、次のように [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証よりも優れている点があります。

- ユーザーは、パスワードの入力を求められることなく、シングル サインオンで認証されます。
- AD グループのログインを作成することで、AD グループのメンバーシップを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のアクセスとアクセス許可を管理できます。  
- 各ユーザーは組織全体で 1 つの ID を持っているため、どの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ログインがどのユーザーに対応しているかを追跡する必要はありません。   
- AD を使用すると、組織全体に一元的なパスワード ポリシーを適用できます。

## <a name="configuration-steps"></a>構成の手順

Active Directory 認証を使用するには、ネットワーク上に AD ドメイン コントローラー (Windows) が必要です。

AD 認証を構成する方法の詳細については、チュートリアルの「[チュートリアル:SQL Server on Linux で Active Directory 認証を使用する](sql-server-linux-active-directory-authentication.md)」を参照してください。 次の一覧は、チュートリアルの各セクションへのリンクが指定された概要です。

1. [SQL Server ホストを Active Directory ドメインに参加させる](sql-server-linux-active-directory-join-domain.md)。
1. [SQL Server 用に AD ユーザーを作成し、ServicePrincipalName を設定する](sql-server-linux-active-directory-authentication.md#createuser)。
1. [SQL Server サービス キータブを構成する](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [キータブ ファイルをセキュリティで保護する](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [Kerberos 認証にキータブ ファイルを使用するように SQL Server を構成する](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [Transact-SQL に AD ベースの SQL Server ログインを作成する](sql-server-linux-active-directory-authentication.md#createsqllogins)。
1. [AD 認証を使用して SQL Server に接続する](sql-server-linux-active-directory-authentication.md#connect)。

## <a name="known-issues"></a>既知の問題

- 現時点では、データベース ミラーリング エンドポイントでサポートされている唯一の認証方法は CERTIFICATE です。 Windows 認証方法は今後のリリースで有効になる予定です。

## <a name="next-steps"></a>次の手順

SQL Server on Linux に Active Directory 認証を実装する方法の詳細については、「[チュートリアル:SQL Server on Linux で Active Directory 認証を使用する](sql-server-linux-active-directory-authentication.md)」を参照してください。
