---
title: サーバーのプロパティ ([セキュリティ] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.security.f1
ms.assetid: b8a131c7-e7bd-4203-bf26-234f1ebfe622
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 11a8e63d75f4194727344009dfac6f2fed77edaa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031427"
---
# <a name="server-properties---security-page"></a>[サーバーのプロパティ] - [セキュリティ] ページ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このページを使用すると、サーバー セキュリティ オプションを表示したり変更したりできます。  
  
## <a name="server-authentication"></a>[サーバー認証]  
 **[Windows 認証モード]**  
 Windows 認証を使用して、試行された接続を検証します。 セキュリティ モードが変更されたときに **sa** パスワードが空白の場合、ユーザーに **sa** パスワードの入力を求めるメッセージが表示されます。  
  
> [!IMPORTANT]  
>  Windows 認証は、SQL Server 認証よりもはるかに安全性に優れています。 可能な場合は、Windows 認証を使用することをお勧めします。  
  
 **[SQL Server 認証モードと Windows 認証モード]**  
 旧バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]との互換性を維持するために、混合モード認証を使用して接続試行を検証します。 セキュリティ モードが変更されたときに **sa** パスワードが空白の場合、ユーザーに **sa** パスワードの入力を求めるメッセージが表示されます。  
  
> [!NOTE]  
>  セキュリティ構成を変更するには、サービスを再起動する必要があります。 [サーバー認証] を [SQL Server 認証モードと Windows 認証モード] に変更する場合、SA アカウントは自動的に有効にはなりません。 SA アカウントを使用するには、ENABLE オプションを指定して [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) を実行します。  
  
## <a name="login-auditing"></a>[ログインの監査]  
 **なし**  
 ログインの監査をオフにします。  
  
 **[失敗したログインのみ]**  
 成功しなかったログインのみを監査します。  
  
 **[成功したログインのみ]**  
 成功したログインのみを監査します。  
  
 **[失敗したログインと成功したログインの両方]**  
 すべてのログイン試行を監査します。  
  
> [!NOTE]  
>  監査レベルを変更するには、サービスを再起動する必要があります。  
  
## <a name="server-proxy-account"></a>[サーバーのプロキシ アカウント]  
 **[サーバーのプロキシ アカウントを有効にする]**  
 **xp_cmdshell**で使用されるアカウントを有効にします。 オペレーティング システム コマンドの実行中に、プロキシ アカウントを使用してログイン、サーバー ロール、データベース ロールの権限を借用します。  
  
> [!CAUTION]  
>  サーバー プロキシ アカウントで使用されるログインには、目的の操作を実行するための必要最低限の権限を与えます。 プロキシ アカウントに過度の権限を与えると、悪意あるユーザーに利用され、システム セキュリティが脅かされる可能性があります。  
  
 **[プロキシ アカウント]**  
 使用されるプロキシ アカウントを指定します。  
  
 **パスワード**  
 プロキシ アカウントのパスワードを指定します。  
  
## <a name="options"></a>オプション  
 **[C2 監査トレースを有効にする]**  
 ステートメントおよびオブジェクトへのアクセスの試行をすべて監査し、\MSSQL\Data ディレクトリ ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既定のインスタンスの場合)、または \MSSQL$*instancename*\Data ディレクトリ ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の名前付きインスタンスの場合) のファイルに記録します。 詳細については、「 [c2 audit mode サーバー構成オプション](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)」を参照してください。  
  
 **[複数データベース間で所有権を連係する]**  
 オンにすると、データベースを複数データベースにまたがる所有権のソースまたはターゲットにすることができます。 詳細については、「 [cross db ownership chaining サーバー構成オプション](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
