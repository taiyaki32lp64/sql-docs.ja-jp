---
title: Reporting Services SharePoint サービス アプリケーションのバックアップと復元 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 93f3eb7db9c00f98d1d4270e9febc105eb6ef6b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574344"
---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Reporting Services SharePoint サービス アプリケーションのバックアップと復元

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

このトピックでは、SharePoint サーバーの全体管理または PowerShell を使用して、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションをバックアップおよび復元する方法について説明します。

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

## <a name="before-you-begin"></a>アンインストールの準備

### <a name="limitations-and-restrictions"></a>制限事項と制約事項

> [!NOTE]
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションは、SharePoint のバックアップおよび復元機能を使用して、部分的にバックアップおよび復元できます。 これには**追加の手順が必要** であり、その手順はこのトピック内に記載されています。 現在、バックアップ プロセスでは、自動実行アカウント (UEA) または Windows 認証用の暗号化キーと資格情報は [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データベースにバックアップ**されません**。

### <a name="recommendations"></a>推奨事項
  
-   SharePoint のバックアップを開始する前に、暗号化キーをバックアップしてください。 暗号化キーをバックアップしなかった場合は、サービス アプリケーションの復元後に、暗号化されたデータへアクセスできなくなります。 その場合、暗号化されたデータを削除する必要が生じます。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションがデータベースへのアクセス用に UEA または Windows 認証を使用しているかどうかを確認してください。 これらのいずれかを使用している場合は、復元プロセス後にサービス アプリケーションを正しく構成できるよう、適切な資格情報を確認してください。  
  
-   SharePoint のバックアップ ログが、バックアップ ファイルと同じフォルダーに作成されていることを確認してください。 このファイルは通常、 **spbackup.log**という名前になります。  
  
## <a name="back-up-the-service-application"></a>サービス アプリケーションのバックアップ

 次の手順を実行します。  
  
1.  暗号化キーのバックアップ  
  
2.  サービス アプリケーションのバックアップ  
  
3.  サービス アプリケーションがデータベースへのアクセス用に UEA または Windows 認証を使用しているかどうかを確認します。 使用している場合は、復元後にサービス アプリケーションを正しく構成できるよう、必要な資格情報をメモします。  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>SharePoint サーバーの全体管理を使用して暗号化キーをバックアップする

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 暗号化キーをバックアップする方法の詳細については、「[Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)」の暗号化キーに関するセクションを参照してください。  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>SharePoint サーバーの全体管理を使用してサービス アプリケーションをバックアップする

サービス アプリケーションをバックアップするには、次の手順を実行します。  
  
1.  SharePoint サーバーの全体管理で、 **[バックアップおよび復元]** グループの **[バックアップの実行]** を選択します。  
  
2.  **[共有サービス]** ノードで、 **[共有サービス アプリケーション]** を展開し、サービス アプリケーションを選択します。 種類は **[SQL Server Reporting Services サービス アプリケーション]** になります。  
  
3.  **[次へ]** を選択します。  
  
4.  **[バックアップの場所]** にパスを入力し、 **[バックアップの開始]** を選択します。  
  
5.  上記のプロセスを繰り返します。ただし、サービス アプリケーションを選択する代わりに、 **[共有サービス プロキシ]** ノードを展開し、サービス アプリケーション プロキシを選択します。 種類は **[SQL Server Reporting Services サービス アプリケーション プロキシ]** になります。  
  
 詳細については、 SharePoint のドキュメントの次のトピックを参照してください。  
  
 [サービス アプリケーションのバックアップ (SharePoint Foundation 2010) (SharePoint ドキュメント)](https://msdn.microsoft.com/library/ee748601.aspx)。  
  
 [サービス アプリケーションのバックアップ (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>実行アカウントとデータベース認証の確認

 **実行アカウント** : サービス アプリケーションが実行アカウントを使用しているかどうかを確認するには、次の手順を実行します。  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション管理]** グループの **[サービス アプリケーションの管理]** を選びます。  
  
2.  サービス アプリケーションの名前を選択し、SharePoint リボンで **[管理]** を選択します。  
  
3.  **[実行アカウント]** を選択します。  
  
4.  実行アカウントが構成されている場合は、サービス アプリケーションのバックアップを復元する際に資格情報が必要になります。 必ず、正しい資格情報を確認してからバックアップおよび復元の手順に進んでください。  
  
 **データベース認証** : サービス アプリケーションがデータベース認証用に Windows 認証を使用しているかどうかを確認するには、次の手順を実行します。  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション管理]** グループの **[サービス アプリケーションの管理]** を選びます。  
  
2.  サービス アプリケーションの名前を選択し、SharePoint リボンで **[プロパティ]** を選択します。  
  
3.  **[Reporting Services (SSRS) サービス データベース]** セクションの内容を確認します。  
  
4.  Windows 認証が構成されている場合は、サービス アプリケーションを復元後に構成する際、資格情報が必要になります。 必ず、正しい資格情報を確認してからバックアップおよび復元の手順に進んでください。  
  
## <a name="restore-the-service-application"></a>サービス アプリケーションの復元

 次の手順を実行します。  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを復元します。  
  
2.  暗号化キーを復元します。  
  
3.  サービス アプリケーションがデータベースへのアクセス用に実行アカウントまたは Windows 認証を使用していた場合は、資格情報を構成します。  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>SharePoint サーバーの全体管理を使用してサービス アプリケーションを復元する
  
1.  SharePoint サーバーの全体管理で、 **[バックアップおよび復元]** グループの **[バックアップからの復元を実行する]** を選択します。  
  
2.  **[バックアップ ディレクトリの場所]** ボックスにバックアップ ファイルのパスを入力し、 **[更新]** を選択します。  
  
3.  **[トップ コンポーネント]** ボックスの一覧からサービス アプリケーションのバックアップを選択し、 **[次へ]** を選択します。  
  
4.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションを選択し、 **[次へ]** を選択します。  
  
5.  **[ログイン名とパスワード]** セクションで、ログイン名のパスワードを入力します。 ログイン名ボックスには、サービス アプリケーションがバックアップ以前に使用していたログインが自動入力されます。  
  
6.  **[復元の開始]** を選択します。  
  
7.  上記のプロセスを繰り返します。ただし、サービス アプリケーションを復元する代わりに、 **[共有サービス]** ノードを展開し、 **[共有サービス アプリケーション]** ノードを展開します。  
  
 詳細については、 SharePoint のドキュメントの次のトピックを参照してください。  
  
 [サービス アプリケーションを復元する (SharePoint Foundation 2010)](https://msdn.microsoft.com/library/ee748615.aspx)。  
  
 [サービス アプリケーションを復元する (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx)。  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>SharePoint サーバーの全体管理を使用して暗号化キーを復元する

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 暗号化キーを復元する方法の詳細については、「[Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)」の暗号化キーに関するセクションを参照してください。  

### <a name="configure-the-execution-account-and-database-authentication"></a>実行アカウントとデータベース認証の構成

 **実行アカウント** : サービス アプリケーションが実行アカウントを使用していた場合は、次の手順を実行して実行アカウントを構成します。  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション管理]** グループの **[サービス アプリケーションの管理]** を選びます。  
  
2.  サービス アプリケーションの名前を選択し、SharePoint リボンで **[管理]** を選択します。  
  
3.  **[実行アカウント]** を選択します。  
  
4.  アカウントとパスワードを入力し、 **[実行アカウントの指定]** ボックスを選択します。  
  
5.  **[OK]** を選択します。  
  
 **データベース認証** : サービス アプリケーションがデータベース認証用に Windows 認証を使用していた場合は、次の手順を実行します。  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション管理]** グループの **[サービス アプリケーションの管理]** を選びます。  
  
2.  サービス アプリケーションの名前を選択し、SharePoint リボンで **[プロパティ]** を選択します。  
  
3.  **[Reporting Services (SSRS) サービス データベース]** セクションの内容を確認します。  
  
4.  **[Windows 認証]** をクリックします。  
  
5.  アカウントとパスワードを入力します。 必要に応じて、 **[Windows 資格情報として使用する]** を選択します。  
  
6.  **[OK]** を選択します。

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
