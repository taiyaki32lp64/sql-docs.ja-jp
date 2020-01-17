---
title: '[サーバーへの接続] (データベース エンジン) | Microsoft Docs'
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 473362544549206a2cfa4183c8e51cd8a399f06e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265112"
---
# <a name="connect-to-server-database-engine"></a>[サーバーへの接続] \(データベース エンジン)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
このダイアログを使用すると、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]に接続するときのオプションを表示または指定できます。 ほとんどの場合、 **[サーバー名]** ボックスにデータベース サーバーのコンピューター名を入力し、 **[接続]** をクリックすることで接続できます。 名前付きインスタンスに接続する場合は、コンピューター名の後に円記号、その後にインスタンスの名前を使用します。 たとえば、 `mycomputer\myinstance`のようにします。 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]に接続している場合、コンピューター名の後に **\sqlexpress**を付けて使用します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続する機能に影響する要因は多数あります。 ヘルプのための次のリソースが見つかりません。  
- [チュートリアル レッスン 1:データベース エンジンへの接続](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [SQL Server データベース エンジンへの接続のトラブルシューティング](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [SQL Server への接続エラーの解決](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)   
  
## <a name="options"></a>オプション  
**サーバーの種類**  
オブジェクト エクスプローラーからサーバーを登録するときは、接続するサーバーの種類 ( [!INCLUDE[ssDE](../../includes/ssde_md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、または [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]) を選択します。 ダイアログの残りの部分には、選択したサーバーの種類に該当するオプションだけが表示されます。 [登録済みサーバー] を使用してサーバーを登録する場合、 **[サーバーの種類]** ボックスは読み取り専用になり、[登録済みサーバー] コンポーネントに表示されているサーバーの種類と一致する値が表示されます。 別の種類のサーバーを登録するには、新しいサーバーの登録を開始する前に、[登録済みサーバー] ツール バーの [ [!INCLUDE[ssDE](../../includes/ssde_md.md)]]、[ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]]、[ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]]、[ [!INCLUDE[ssEW](../../includes/ssew-md.md)]]、または [ [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ] をクリックします。  
  
**[サーバー名]**  
接続するサーバー インスタンスを選択します。 既定では、最後に接続していたサーバー インスタンスが表示されます。  
  
> [!NOTE]  
> [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] のアクティブなユーザー インスタンスに接続するには、`np:\\.\pipe\3C3DF6B1-2262-47\tsql\query` などの、パイプ名を指定する名前付きパイプ プロトコルを使用して接続します。 詳細については、[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] のドキュメントを参照してください。  
> [!NOTE]  
> 接続は、通常、"最近使用した (MRU)" の履歴で保持されます。 MRU からエントリを削除するには、 **[サーバー名]** コンボ ボックス上をクリックし、削除するサーバーの名前を選択し、**DEL** キーを押すだけです。  
   
**[認証]**  
SSMS の現在のバージョンでは、[!INCLUDE[ssDE](../../includes/ssde_md.md)] のインスタンスへの接続時に 5 つの認証モードを用意しています。 認証ダイアログ ボックスが次の一覧と一致しない場合は、[SQL Server Management Studio (SSMS) のダウンロード](../download-sql-server-management-studio-ssms.md) から SSMS の最新のバージョンをダウンロードします。  

  
> **[Windows 認証]**  
> [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 認証モードを使用すると、ユーザーは Windows ユーザー アカウントを使用して接続できます。  
> 
> **SQL Server 認証 (SQL Server Authentication)**  
> 指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで認証を行います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログイン アカウントが設定されていない場合、認証は失敗し、エラー メッセージが返されます。 可能であれば、Windows 認証または Active Directory - パスワード認証を使用します。  
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
  
**のインスタンスに接続するときには、**  
クリックしてサーバーに接続します。  
  
**[オプション]**  
クリックして、[**接続プロパティ**] タブ、および [**追加の接続パラメーター**] タブを表示します。  
  
