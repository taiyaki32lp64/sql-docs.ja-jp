---
title: '[サーバーへの接続] ([ログイン] ページ) (データベース エンジン) | Microsoft Docs'
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c3d6f51174198474046eb8c5a6155270a1445ccc
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265091"
---
# <a name="connect-to-server-login-page-database-engine"></a>[サーバーへの接続] \([ログイン] ページ) (データベース エンジン)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
このタブを使用すると、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]に接続するときのオプションを表示または指定できます。 ほとんどの場合、 **[サーバー名]** ボックスにデータベース サーバーのコンピューター名を入力し、 **[接続]** をクリックすることで接続できます。 名前付きインスタンスに接続する場合は、コンピューター名の後に円記号、その後にインスタンスの名前を使用します。 たとえば、 `mycomputer\myinstance`のようにします。 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]に接続している場合、コンピューター名の後に **\sqlexpress**を付けて使用します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続する機能に影響する要因は多数あります。 ヘルプのための次のリソースが見つかりません。  
- [チュートリアル レッスン 1:データベース エンジンへの接続](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [SQL Server データベース エンジンへの接続のトラブルシューティング](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [SQL Server への接続エラーの解決](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)    
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証で接続するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証モードと Windows 認証モードで構成する必要があります。 認証モードの決定方法と認証モードの変更方法の詳細については、「[方法:サーバーの認証モードの変更](../../database-engine/configure-windows/change-server-authentication-mode.md)」を参照してください。  
  
## <a name="options"></a>オプション  
**サーバーの種類**  
オブジェクト エクスプローラーからサーバーを登録するときに、接続するサーバーの種類 ( [!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services、または Integration Services) を選択します。 ダイアログ ボックスのその他の領域には、選択したサーバーの種類に該当するオプションだけが表示されます。 [登録済みサーバー] を使用してサーバーを登録する場合、 **[サーバーの種類]** ボックスは読み取り専用になり、[登録済みサーバー] コンポーネントに表示されているサーバーの種類と一致する値が表示されます。 別の種類のサーバーを登録するには、新しいサーバーの登録を開始する前に、[登録済みサーバー] ツール バーの [ [!INCLUDE[ssDE](../../includes/ssde_md.md)]]、[Analysis Services]、[Reporting Services]、または [Integration Services] を選択します。  
  
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] を通じて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンのインスタンスに接続する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用し、 **[サーバーへの接続]** ダイアログ ボックスの **[接続プロパティ]** タブでデータベースを指定する必要があります。 **[暗号化接続]** チェック ボックスがオンになっていることを確認してください。  
  
既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **master**に接続されます。 ユーザー データベースを指定すると、オブジェクト エクスプローラーにそのデータベースとそのオブジェクトのみが表示されます。 **master** に接続すると、すべてのデータベースを表示できるようになります。 詳しくは、[Microsoft Azure SQL Database の概要](/azure/sql-database/sql-database-technical-overview/)に関する記事をご覧ください。
  
**サーバー名**  
接続するサーバー インスタンスを選択します。 既定では、最後に接続していたサーバー インスタンスが表示されます。  
  
**[認証]**  
SSMS の現在のバージョンでは、[!INCLUDE[ssDE](../../includes/ssde_md.md)] のインスタンスへの接続時に 5 つの認証モードを用意しています。 認証ダイアログ ボックスが次の一覧と一致しない場合は、[SQL Server Management Studio (SSMS) のダウンロード](../download-sql-server-management-studio-ssms.md) から SSMS の最新のバージョンをダウンロードします。     
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] を通じて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンのインスタンスに接続する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用し、 **[サーバーへの接続]** ダイアログ ボックスの **[接続プロパティ]** タブでデータベースを指定する必要があります。 **[暗号化接続]** チェック ボックスがオンになっていることを確認してください。  
  
既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **master**に接続されます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] に接続する場合にユーザー データベースを指定すると、オブジェクト エクスプローラーにそのデータベースとそのオブジェクトのみが表示されます。 **master** に接続すると、すべてのデータベースを表示できるようになります。 詳しくは、[Microsoft Azure SQL Database の概要](/azure/sql-database/sql-database-technical-overview/)に関する記事をご覧ください。  
  
> **[Windows 認証]**  
> [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 認証モードを使用すると、ユーザーは Windows ユーザー アカウントを使用して接続できます。  
> 
> **SQL Server 認証 (SQL Server Authentication)**  
> 指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで認証を行います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログイン アカウントが設定されていない場合、認証は失敗し、エラー メッセージが返されます。 可能な場合は、Windows 認証を使用します。  
> 
> **Active Directory - Active Directory - MFA で汎用のサポート**  
> [Active Directory - MFA で汎用] は、Azure Multi-Factor Authentication (MFA) をサポートする対話型ワークフローです。 Azure MFA を使えば、簡単なサインイン プロセスというユーザーの要求を満たしながら、データとアプリケーションへのアクセスを保護できます。 電話、テキスト メッセージ、スマート カードと PIN、モバイル アプリ通知などの簡単な検証オプションで強力な認証を提供し、ユーザーが好みの方法を選択できるようにします。 ユーザー アカウントが MFA 用に構成されている場合の対話型認証ワークフローでは、ポップアップ ダイアログ ボックスやスマート カードなどを使用する追加のユーザー対話が必要です。ユーザー アカウントが MFA 用に構成されている場合、ユーザーは Azure ユニバーサル認証を選択して接続する必要があります。 ユーザー アカウントに MFA が必要ない場合は、ユーザーは他の 2 つの Azure Active Directory 認証オプションを使用できます。 詳細については、「 [SQL Database と SQL Data Warehouse での Azure AD MFA のための SSMS のサポート](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)」をご覧ください。 必要に応じて、ログインを認証するドメインを変更することができます。そのためには、[**オプション**] をクリックし、[**接続プロパティ**] タブを選択し、[**AD ドメイン名またはテナント ID**ボックス] に入力します。  
> 
> **Active Directory - パスワード**  
> Azure Active Directory 認証は、Azure Active Directory (Azure AD) の ID を使用して [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] に接続するメカニズムです。  Azure とフェデレーションされていないドメインから資格情報を使用して Windows にログインしている場合、あるいは初期ドメインまたはクライアント ドメインに基づく Azure AD を使用する Azure AD 認証を使用している場合は、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] への接続にこの方法を使用します。 詳細については、「 [Azure Active Directory 認証を使用して SQL Database に接続する](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)」を参照してください。  
> 
> **Active Directory - 統合**  
> Azure Active Directory 認証は、Azure Active Directory (Azure AD) の ID を使用して [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] に接続するメカニズムです。 フェデレーション ドメインから Azure Active Directory の資格情報を使用して Windows にログインしている場合は、この方法を使用して [!INCLUDE[ssSDS](../../includes/sssds-md.md)] に接続します。 詳細については、「 [Azure Active Directory 認証を使用して SQL Database に接続する](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)」を参照してください。  
  
**User name**  
接続に使用する Windows ユーザー名です。 このオプションは、 **Active Directory パスワード認証**を使用した接続が指定されている場合にのみ使用できます。 [**Windows 認証**] または [**Active Directory - 統合**] 認証を選択した場合は、読み取り専用となります。  
  
**Login**  
接続に使用するログインを入力します。 このオプションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証または Active Directory パスワード認証を使用した接続が指定されている場合にのみ使用できます。  
  
**Password**  
ログインのパスワードを入力します。 このオプションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証または Active Directory - パスワード認証を使用した接続が指定されている場合にのみ編集できます。  
  
**[パスワードを保存する]**  
入力したパスワードを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に記憶させるには、このチェック ボックスをオンにします。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合だけ表示されます。  
  
**のインスタンスに接続するときには、**  
クリックしてサーバーに接続します。  
  
**[オプション]**  
クリックして、[**接続プロパティ**] タブ、および [**追加の接続パラメーター**] タブを表示します。  
   
  
