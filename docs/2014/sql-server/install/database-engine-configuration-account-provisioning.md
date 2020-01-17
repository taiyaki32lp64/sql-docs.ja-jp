---
title: データベース エンジンの構成 - アカウントの準備 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 834b26bc-49de-4033-88d5-6aa7b1609720
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 300e3dd81ae7a3de2361c79864130c1361c19588
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095873"
---
# <a name="database-engine-configuration---account-provisioning"></a>データベース エンジンの構成 - アカウントの準備
  このページは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ モードを設定し、Windows ユーザーまたはグループを [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の管理者として追加するために使用します。  
  
## <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の実行に関する注意点  
 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 **のログインとして** BUILTIN\Administrators [!INCLUDE[ssDE](../../includes/ssde-md.md)] グループが準備され、ローカル Administrators グループのメンバーは、管理者資格情報を使用してログインできました。 しかし、引き上げられたアクセス許可を使用するのはベスト プラクティスではありません。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 **BUILTIN\Administrators** グループはログインとして準備されていません。 したがって、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンスのインストール時に、管理ユーザーごとに [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ログインを作成し、そのログインを sysadmin 固定サーバー ロールに追加する必要があります。 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの実行に使用する Windows アカウントに対しても、同様の操作を行う必要があります。 それらのジョブには、レプリケーション エージェント ジョブも含まれます。  
  
## <a name="options"></a>および  
 **[セキュリティ モード]** : インストール用に Windows 認証または混合モード認証を選択します。  
  
 **[Windows プリンシパルの準備]** : 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、Windows の Builtin\Administrator ローカル グループが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin サーバー ロールに配置されました。これは、Windows 管理者に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスへのアクセス許可を付与する効果的な方法でした。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、Builtin\Administrator グループは sysadmin  サーバー ロールで提供されません。 代わりに、セットアップ時に新規インストール用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者を明示的に用意する必要があります。  
  
> [!IMPORTANT]  
>  セットアップ時に新規インストール用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者を明示的に用意する必要があります。 セットアップは、この手順を完了するまで続行できません。  
  
 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者の指定]** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの Windows プリンシパルを少なくとも 1 つ指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行しているアカウントを追加するには、 **[現在のユーザー]** ボタンをクリックします。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスについて管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。  
  
 一覧の編集が完了したら、 **[OK]** をクリックし、構成ダイアログ ボックスで管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** をクリックします。  
  
 混合モード認証を選択した場合は、組み込みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者 (SA) アカウントのログオン資格情報を入力する必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Windows 認証モード**  
 Windows ユーザー アカウントでユーザーが接続すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はオペレーティング システムの Windows プリンシパル トークンを使用してアカウント名とパスワードを検証します。 これは既定の認証モードで、混合モードよりはるかに安全性に優れています。 Windows 認証では、Kerberos セキュリティ プロトコルを利用し、強力なパスワードに対して複雑な検証を行うという点で、パスワード ポリシーが強化されています。また、アカウント ロックアウトの機能を提供し、パスワード有効期限にも対応しています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]sa パスワードを空白のままにしないでください。また、推測しやすいパスワードを設定しないでください。  
  
 **混合モード (Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証)**  
 Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用してユーザー接続を許可します。 Windows ユーザー アカウントで接続するユーザーは、Windows によって検証される信頼関係接続を使用することができます。  
  
 混合モード認証を選択する必要があり、レガシ アプリケーションに対応するために SQL ログインを使用する必要もある場合は、必ずすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントに強力なパスワードを設定してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証は旧バージョンとの互換性を維持するためだけに提供されます。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **パスワードの入力**  
 システム管理者 (sa) ログインを入力および確認します。 パスワードは侵入者に対する防御の最前線であるため、システムのセキュリティにとって強力なパスワードを設定することは不可欠です。 sa パスワードを空白のままにしないでください。また、推測しやすいパスワードを設定しないでください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パスワードは、文字、記号、数字の組み合わせを含む 1 ～ 128 文字で指定できます。 混合モード認証を選択する場合、インストール ウィザードの次のページに進む前に、強力な sa パスワードを入力する必要があります。  
  
 **強力なパスワードのガイドライン**  
 強力なパスワードとは、他人によってたやすく推測されず、コンピューター プログラムを使用して簡単にはハッキングされないパスワードです。 強力なパスワードでは、次のような禁止された条件または用語を使用することはできません。  
  
-   空白または NULL 条件  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   "sysadmin"  
  
 強力なパスワードには、インストール コンピューターに関連付けられた次のような用語を指定できません。  
  
-   現在、マシンにログオンしているユーザーの名前  
  
-   コンピューター名  
  
 強力なパスワードは、長さ 9 文字以上で、以下の 4 つの条件のうち 3 つ以上を満たしている必要があります。  
  
-   大文字を含んでいる。  
  
-   小文字を含んでいる。  
  
-   数字を含んでいる。  
  
-   #、%、^ など、英数字以外の文字を含んでいる。  
  
 このページで入力するパスワードは、強力なパスワード ポリシーの要件を満たす必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用したオートメーションを使用している場合、必ず強力なパスワード ポリシーの要件を満たすパスワードを指定してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 Windows 認証と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のどちらを選択するかについて詳しくは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「**認証モードの選択**」を参照してください。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]を実行するアカウントの選択の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「**Windows サービス アカウントと権限の構成**」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
