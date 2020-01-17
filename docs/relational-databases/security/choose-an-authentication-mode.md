---
title: 認証モードの選択 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.ins.instwizard.authenticationmode.f1
- sql13.swb.passwordexpired.f1
helpviewer_keywords:
- sa account
- authentication modes
- trusted connection
- SQL Server Installation Wizard, Authentication Mode page
- choose authentication mode
- authentication [SQL Server], choosing a mode
- Windows authentication [SQL Server]
- mixed mode authentication
- mixed authentication mode
- SQL authentication mode
- Password Expired dialog box
ms.assetid: ff7a6a48-3d38-4209-aa0f-7d6c0a8c64ef
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: caee3b1fab893e456a5a781641b6cf70222b16ff
ms.sourcegitcommit: 0d5b0aeee2a2b34fd448aec2e72c0fa8be473ebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75721357"
---
# <a name="choose-an-authentication-mode"></a>認証モードの選択
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  セットアップ中に、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の認証モードを選択する必要があります。 選択できるモードは、Windows 認証モードと混合モードの 2 つです。 Windows 認証モードを選択すると、Windows 認証が有効になり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が無効になります。 混合モードを選択すると、Windows 認証と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証の両方が有効になります。 Windows 認証は常に使用可能であり、無効にすることはできません。  
  
## <a name="configuring-the-authentication-mode"></a>認証モードの構成  
 セットアップ中に混合モード認証を選択した場合は、sa という組み込みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウントの強力なパスワードを入力して確認する必要があります。 sa アカウントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続します。  
  
 セットアップ中に Windows 認証を選択した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証用に sa アカウントが作成されますが、無効になっています。 後で混合モード認証に変更し、sa アカウントを使用する場合に、アカウントを有効にする必要があります。 任意の Windows アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントは、システム管理者として構成できます。 sa アカウントはよく知られているため、悪意のあるユーザーの攻撃対象となることが少なくありません。そのため、アプリケーションで必要とならない限り、sa アカウントを有効にしないでください。 また、sa アカウントでは、パスワードを空白のままにしたり、推測しやすいパスワードを設定しないでください。 Windows 認証モードから混合モード認証に変更して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、「 [サーバーの認証モードの変更](../../database-engine/configure-windows/change-server-authentication-mode.md)」をご覧ください。  
  
## <a name="connecting-through-windows-authentication"></a>Windows 認証を使用した接続  
 Windows ユーザー アカウントでユーザーが接続すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はオペレーティング システムの Windows プリンシパル トークンを使用してアカウント名とパスワードを検証します。 つまり、ユーザーの ID は Windows によって確認されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、パスワードが要求されず、ID の検証も行われません。 Windows 認証は、既定の認証モードであり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証よりもはるかに安全性に優れています。 Windows 認証では、Kerberos セキュリティ プロトコルを利用し、強力なパスワードに対して複雑な検証を行うという点に関して、パスワード ポリシーが強化されています。また、アカウント ロックアウトの機能を提供し、パスワード有効期限にも対応しています。 Windows 認証を使用して行われた接続は、信頼関係接続と呼ばれることがあります。これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では Windows が提供する資格情報を信頼しているためです。  
  
 Windows 認証を使用することにより、Windows グループをドメイン レベルで作成できます。また、グループ全体に対して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログインを作成できます。 ドメイン レベルでアクセスを管理すると、アカウント管理を簡素化できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="connecting-through-sql-server-authentication"></a>SQL Server 認証を使用した接続  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用すると、Windows ユーザー アカウントに基づかないログインが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に作成されます。 ユーザー名とパスワードの両方が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して作成され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続するユーザーは、接続するたびに資格情報 (ログインとパスワード) を入力する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントに強力なパスワードを設定する必要があります。 強力なパスワードのガイドラインについては、「 [強力なパスワード](../../relational-databases/security/strong-passwords.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインでは、省略可能な 3 つのパスワード ポリシーを使用できます。  
  
-   [ユーザーは次回ログイン時にパスワードを変更する]  
  
     ユーザーは、次回接続するときにパスワードを変更する必要があります。 パスワードを変更する機能は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]に用意されています。 このオプションが使用されている場合、サード パーティのソフトウェア開発者はこの機能を提供する必要があります。  
  
-   [パスワードの期限を適用する]  
  
     コンピューターのパスワードの有効期限ポリシーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに適用されます。  
  
-   [パスワード ポリシーを適用する]  
  
     コンピューターの Windows のパスワード ポリシーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに適用されます。 これには、パスワードの長さおよび複雑さが含まれます。 この機能は、 `NetValidatePasswordPolicy` 以降のバージョンのみで使用できる [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] API に依存します。  
  
#### <a name="to-determine-the-password-policies-of-the-local-computer"></a>ローカル コンピューターのパスワード ポリシーを確認するには  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。  
  
2.  **[ファイル名を指定して実行]** ダイアログ ボックスで、「 **secpol.msc**」と入力し、 **[OK]** をクリックします。  
  
3.  **[ローカル セキュリティ設定]** アプリケーションで、 **[セキュリティの設定]** 、 **[アカウント ポリシー]** の順に展開して、 **[パスワードのポリシー]** をクリックします。  

     結果ペインに、パスワードのポリシーが表示されます。  
  
### <a name="disadvantages-of-sql-server-authentication"></a>SQL Server 認証の欠点  
  
-   Windows のログインとパスワードを持っている Windows ドメイン ユーザーの場合、接続するために別の ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) ログインとパスワードを入力する必要があります。 多くのユーザーにとって、複数の名前とパスワードを把握しておくことは困難です。 データベースに接続するたびに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の資格情報を入力する必要があるのは面倒な場合があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証では、Kerberos セキュリティ プロトコルを使用できません。  
  
-   Windows には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインで使用できない、追加のパスワード ポリシーが用意されています。  
  
-   接続時に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインの暗号化されたパスワードをネットワーク上で渡す必要があります。 自動的に接続する一部のアプリケーションでは、クライアントでパスワードが保存されます。 これらは追加の攻撃ポイントとなります。  
  
### <a name="advantages-of-sql-server-authentication"></a>SQL Server 認証の利点  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、古いアプリケーションや、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を必要とする、サード パーティが提供するアプリケーションをサポートできます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、すべてのユーザーが Windows ドメインで認証されていない、オペレーティング システムが混在する環境をサポートできます。  
  
-   ユーザーが不明または信頼されていないドメインから接続できる場合。 たとえば、既存の顧客が、割り当てられた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを使用して接続し、発注状況を確認するアプリケーションの場合です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ユーザーが独自の ID を作成する Web ベースのアプリケーションをサポートできます。  
  
-   ソフトウェア開発者は、事前に設定された既知の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに基づいた、複雑な権限の階層を使用してアプリケーションを配布できます。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているコンピューターのローカル管理者の権限は制限されません。  
  
## <a name="see-also"></a>参照  
 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
