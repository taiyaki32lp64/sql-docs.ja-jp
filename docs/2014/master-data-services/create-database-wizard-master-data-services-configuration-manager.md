---
title: データベースの作成ウィザード (マスター データ サービス構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7207cd8e3a087ed0aa85931254754d4009d73c53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479870"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>データベースの作成ウィザード (マスター データ サービス構成マネージャー)
  **データベースの作成** ウィザードを使用して、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースを作成します。  
  
## <a name="database-server"></a>[データベース サーバー]  
 ローカルまたはリモートの [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] インスタンスに接続して [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースをホストするための情報を指定します。 リモート インスタンスに接続するには、そのインスタンスでリモート接続を有効にする必要があります。  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**SQL Server インスタンス (SQL Server instance)**|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] データベースをホストするために必要な [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インスタンス名を指定します。 ここには、ローカルまたはリモートのコンピューターの、既定または名前付きのインスタンスを指定できます。 次のように入力して、情報を指定します。<br /><br /> ローカル コンピューター上の既定のインスタンスに接続するには、ピリオド (.) を入力します。<br /><br /> 指定したローカル コンピューターまたはリモート コンピューター上の既定のインスタンスに接続するには、サーバー名または IP アドレスを入力します。<br /><br /> 指定したローカル コンピューターまたはリモート コンピューター上の名前付きインスタンスに接続するには、サーバー名または IP アドレスと、インスタンス名を入力します。 この情報は、 *server_name*\\*instance_name*の形式で指定します。|  
|**認証の種類**|指定した SQL Server インスタンスへの接続時に使用する認証の種類を選択します。 接続に使用する資格情報は、指定した **インスタンスの** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サーバー ロールに含まれている必要があります。 sysadmin ロールの詳細については、「 [サーバー レベルのロール](../relational-databases/security/authentication-access/server-level-roles.md)」を参照してください。 認証の種類は次のとおりです。<br /><br /> **[現在のユーザー – 統合セキュリティ]**:現在の Windows ユーザー アカウントの資格情報を使用して接続するときに、統合 Windows 認証を使用します。 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] では、コンピューターにログオンしてアプリケーションを開いたユーザーの Windows 資格情報が使用されます。 アプリケーションで別の Windows 資格情報を指定することはできません。 別の Windows 資格情報を使用して接続する場合は、そのユーザーとしてコンピューターにログオンし、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]を開く必要があります。<br /><br /> **[SQL Server アカウント]**:接続する際に SQL Server アカウントを使用します。 このオプションを選択すると、 **[ユーザー名]** フィールドと **[パスワード]** フィールドが有効になり、指定した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] アカウントの資格情報を指定する必要があります。|  
|**ユーザー名**|指定した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスへの接続に使用されるユーザー アカウントの名前を指定します。 アカウントは、指定した **インスタンスの** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ロールに属している必要があります。<br /><br /> **[認証の種類]** が **[現在のユーザー - 統合セキュリティ]** の場合、**[ユーザー名]** ボックスは読み取り専用で、コンピューターにログオンした Windows ユーザー アカウント名が表示されます。<br /><br /> **[認証の種類]** が **[SQL Server アカウント]** の場合、 **[ユーザー名]** ボックスが有効になり、指定した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] アカウントの資格情報を指定する必要があります。|  
|**Password**|ユーザー アカウントに関連付けられているパスワードを指定します。<br /><br /> **[認証の種類]** が **[現在のユーザー - 統合セキュリティ]** の場合、**[パスワード]** ボックスは読み取り専用で、指定した Windows ユーザー アカウントの資格情報が接続に使用されます。<br /><br /> **[認証の種類]** が **[SQL Server アカウント]** の場合、 **[パスワード]** ボックスが有効になり、指定したユーザー アカウントに関連付けられているパスワードを指定する必要があります。|  
|**[接続テスト]**|指定したユーザー アカウントで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスに接続でき、そのインスタンスの [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースを作成する権限がアカウントに与えられていることを確認します。 **[接続テスト]** をクリックしなかった場合、 **[次へ]** をクリックしたときに接続がテストされます。|  
  
## <a name="database"></a>[データベース]  
 新しいデータベースのデータベース名と照合順序のオプションを指定します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の照合順序により、並べ替え規則、大文字と小文字の区別、およびアクセントの区別のプロパティをデータで利用できるようになります。 char や varchar などの文字データ型に使用する照合順序は、そのデータ型で表すことのできるコード ページおよび対応する文字を指定します。 照合順序の詳細については、「 [照合順序と Unicode のサポート](../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**データベース名**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの名前を指定します。|  
|**[SQL Server の既定の照合順序]**|新しいデータベースに指定した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスの現在のデータベース照合順序の設定を使用する場合に選択します。|  
|**[Windows 照合順序]**|新しいデータベースに使用する Windows 照合順序の設定を指定します。 Windows 照合順序では、関連する Windows ロケールに基づいて文字データを格納するための規則が定義されます。 Windows 照合順序および関連するオプションの詳細については、「[Windows 照合順序名 (Transact-SQL)](/sql/t-sql/statements/windows-collation-name-transact-sql)」を参照してください。<br /><br /> 注:**[Windows 照合順序]** ボックスの一覧と関連するオプションは、**[SQL Server の既定の照合順序]** チェック ボックスをオフにした後にのみ有効になります。|  
  
## <a name="administrator-account"></a>[管理者アカウント]  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**ユーザー名**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] システム管理者にするドメイン ユーザー アカウントを指定します。 すべての[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]このデータベースでは、このユーザーに関連付けられている Web アプリケーションには、すべてのモデルとすべての機能領域のすべてのデータを更新できます。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。|  
  
## <a name="summary"></a>まとめ  
 選択したオプションの概要を表示します。 選択内容を確認して **[次へ]** をクリックすると、指定した設定でデータベースの作成が開始されます。  
  
## <a name="progress-and-finish"></a>[続行して完了する]  
 作成処理の進捗状況を表示します。 データベースが作成されたら、 **[完了]** をクリックしてデータベースのウィザードを終了し、 **[データベース]** ページに戻ります。 新しいデータベースが選択され、そのシステム設定を表示および変更できます。  
  
## <a name="see-also"></a>参照  
 [[データベース構成] ページ (マスター データ サービス構成マネージャー)](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [マスター データ サービスのデータベースと web サイトの設定します。](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [データベース要件 &#40;マスター データ サービス&#41;](install-windows/database-requirements-master-data-services.md)  
  
  
