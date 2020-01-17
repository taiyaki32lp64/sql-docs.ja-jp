---
title: MSSQLSERVER_18456 | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18456 (Database Engine error)
ms.assetid: c417631d-be1f-42e0-8844-9f92c77e11f7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 737e64973e4651dd36c58fa9ff97a61c65a604a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137091"
---
# <a name="mssqlserver18456"></a>MSSQLSERVER_18456
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|18456|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LOGON_FAILED|  
|メッセージ テキスト|ユーザー '%.*ls'.%.\*ls はログインできませんでした|  
  
## <a name="explanation"></a>説明  
無効なパスワードまたはユーザー名の使用による認証の失敗によって接続の試行が拒否された場合、クライアントに次のようのメッセージが表示されます。"ユーザー '<user_name>' はログインできませんでした。 (Microsoft SQL Server、エラー:18456)"。  
  
クライアントに返される追加情報には、次のようなものがあります。  
  
"ユーザー '<user_name>' はログインできませんでした。 (.Net SqlClient Data Provider)"  
  
-----------------------------\-  
  
"サーバー名: <computer_name>"  
  
"エラー番号:18456"  
  
"重大度:14"  
  
"状態:1"  
  
"行番号:65536"  
  
次のメッセージが返されることもあります。  
  
"メッセージ 18456、レベル 14、状態 1、サーバー <computer_name>、行 1"  
  
"ユーザー '<user_name>' はログインできませんでした。"  
  
## <a name="additional-error-information"></a>エラーに関する追加情報  
セキュリティ向上のために、クライアントに返されるエラー メッセージでは、認証エラーの性質を意図的に非表示にしています。 ただし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログでは、対応するエラーに、認証失敗条件と対応付けられるエラー状態が含まれています。 ログインできない理由を判断するには、エラー状態を次の一覧と比較してください。  
  
|状態|[説明]|  
|---------|---------------|  
|1|エラー情報を表示できません。 通常、この状態は、エラーの詳細情報を受け取る権限がないことを意味します。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者に問い合わせてください。|  
|2|ユーザー ID が無効です。|  
|5|ユーザー ID が無効です。|  
|6|SQL Server 認証で Windows ログイン名を使用しようとしました。|  
|7|ログインが無効で、パスワードが正しくありません。|  
|8|パスワードが正しくありません。|  
|9|パスワードが無効です。|  
|11|ログインは有効ですが、サーバー アクセスに失敗しました。 このエラーで考えられる原因の 1 つは、Windows ユーザーがローカル管理者グループのメンバーとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのアクセス権限を持っている一方で、Windows から管理者資格情報が提供されないことです。 接続するには、 **[管理者として実行]** オプションを使用して接続プログラムを開始してから、その Windows ユーザーを特定のログインとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に追加します。|  
|12|ログインは有効なログインですが、サーバー アクセスに失敗しました。|  
|18|パスワードを変更する必要があります。|  
|38, 46|ユーザーによって要求されたデータベースを見つけることができませんでした。|
|102 - 111|AAD のエラーです。|
|122 - 124|空のユーザー名またはパスワードによるエラーです。|
|126|ユーザーによって要求されたデータベースは存在しません。|
|132 - 133|AAD のエラーです。|
  
エラー状態は他にも存在し、予期しない内部処理エラーを示します。  
  
**その他の特殊な原因**  
  
エラーの理由として、 **"SQL 認証を使用したログインに失敗しました。サーバーは、Windows 認証専用に構成されています。** 次の状況で返される場合があります。  
  
-   サーバーが混合モード認証で構成され、ODBC 接続で TCP プロトコルを使用し、接続でセキュリティ接続を使用することが明示的に指定されていない場合。  
  
-   サーバーが混合認証モードで構成され、ODBC 接続で名前付きパイプが使用され、クライアントで名前付きパイプを開くために使用された資格情報が自動的にユーザーの権限を借用するために使用され、接続でセキュリティ接続を使用することが明示的に指定されていない場合。  
  
この問題を解決するには、接続文字列に **TRUSTED_CONNECTION = TRUE** を含めます。  
  
## <a name="examples"></a>使用例  
この例では、認証エラー状態は 8 です。 これは、パスワードが正しくないことを示します。  
  
|date|Source|メッセージ|  
|--------|----------|-----------|  
|2007-12-05 20:12:56.34|ログオン|エラー:18456、重大度:14、状態:8.|  
|2007-12-05 20:12:56.34|ログオン|ユーザー '<user_name>' はログインできませんでした。 [CLIENT: <ip address>]|  
  
> [!NOTE]  
> Windows 認証モードを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールし、後で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証モードと Windows 認証モードに変更すると、**sa** ログインは最初は無効になります。 これにより、次の状態 7 のエラーが発生します。"ユーザー 'sa' はログインできませんでした。"**sa** ログインを有効にするには、「[サーバーの認証モードの変更](~/database-engine/configure-windows/change-server-authentication-mode.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続しようとしている場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が混合モード認証で構成されていることを確認します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続しようとしている場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが存在し、そのログインのスペルを正しく入力していることを確認します。  
  
Windows 認証を使用して接続しようとしている場合は、正しいドメインに適切にログインしていることを確認します。  
  
エラーが状態 1 を示している場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者に問い合わせてください。  
  
管理者の資格情報を使用して接続する場合、 **[管理者として実行]** オプションを使用してアプリケーションを起動します。 接続したら、Windows ユーザーを個別のログインとして追加します。  
  
[!INCLUDE[ssDE](../../includes/ssde-md.md)]で包含データベースがサポートされる場合、包含データベース ユーザーへの移行後にそのログインが削除されていないことを確認してください。  
  
ローカルの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続している場合、**NT AUTHORITY\NETWORK SERVICE** で実行されているサービスからの接続は、コンピューターの完全修飾ドメイン名を使用して認証する必要があります。 詳細については、このトピックの「[方法: ASP.NET で Network Service アカウントを使用してリソースにアクセスする方法](https://msdn.microsoft.com/library/ff647402.aspx)」を参照してください。  
  
