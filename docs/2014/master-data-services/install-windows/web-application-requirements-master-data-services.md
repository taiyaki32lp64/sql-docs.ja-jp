---
title: Web アプリケーションの要件 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 15b394c836cb24229944f4e0775dfccad847a32b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482884"
---
# <a name="web-application-requirements-master-data-services"></a>Web アプリケーションの要件 (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] は、インターネット インフォメーション サービス (IIS) によってホストされる Web アプリケーションです。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] は Internet Explorer (IE) 7 以降でのみ動作します。 IE 7 以前のバージョン、Microsoft Edge、Chrome はサポートされていません。  
  
 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] Web アプリケーションを作成および構成するには、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] を使用します。 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] は、ローカル コンピューター上の IIS を構成するので、最初に Web 構成タスクを行う場合に最適です。 たとえば、1 つの [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web アプリケーションを使用して [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 環境を構成したり、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]のスケールアウト配置の最初の Web アプリケーションを構成したりします。 スケールアウト配置の複数の Web サーバーの構成など、より複雑なタスクを実行する場合は、IIS ツールを使用します。  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] のコンポーネントをインストールするコンピューターはすべてライセンス供与を受けている必要があります。 詳細については、使用許諾契約書 (EULA) を参照してください。  
  
## <a name="requirements"></a>必要条件  
  
### <a name="operating-system"></a>オペレーティング システム  
 次の Windows オペレーティング システムには、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web アプリケーションおよび Web サービスに必要なインターネット インフォメーション サービス (IIS) の機能が含まれています。  
  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer (64 ビット) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (64 ビット) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence (64 ビット) x64|  
|-------------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows 7 Professional、Enterprise、Ultimate<br /><br /> Windows 8.0 Professional、Enterprise、および Ultimate|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|  
  
 エディションがサポートされている Windows オペレーティング システムの完全な一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)します。  
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションで作業するには、Silverlight 5 をクライアント コンピューターにインストールする必要があります。 Silverlight の必要なバージョンがない場合、Web アプリケーションで Silverlight を使用する部分に移動したときに、Silverlight をインストールするよう要求されます。 Silverlight 5 は [ここ](https://go.microsoft.com/fwlink/?LinkId=243096)からインストールできます。  
  
### <a name="role-and-role-services-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>ロールとロール サービス (Windows Server 2008 または Windows Server 2008 R2、Windows 7 オペレーティング システム)  
 Windows Server 2008 R2 では、Microsoft 管理コンソール (MMC) にある **サーバー マネージャー**を使用して、 **Web サーバー (IIS)** ロールと、次に示す必要なロール サービスをインストールできます。  
  
> [!NOTE]  
>  [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] および Windows 7 オペレーティング システムでは、コントロール パネルの **[プログラムと機能]** を使用して、 **[Windows の機能]** ダイアログ ボックスに表示されるこれらのオプションを有効にします。  
  
||  
|-|  
|Web サーバー<br /><br /> HTTP 基本機能<br /><br /> 静的なコンテンツ<br /><br /> 既定のドキュメント<br /><br /> ディレクトリの参照<br /><br /> HTTP エラー<br /><br /> アプリケーション開発<br /><br /> ASP.NET<br /><br /> .NET 拡張性<br /><br /> ISAPI 拡張<br /><br /> ISAPI フィルター<br /><br /> 状態と診断<br /><br /> HTTP ログ<br /><br /> 要求の監視<br /><br /> セキュリティ<br /><br /> [Windows 認証]<br /><br /> 要求フィルター<br /><br /> パフォーマンス<br /><br /> 静的なコンテンツの圧縮<br /><br /> 管理ツール<br /><br /> IIS 管理コンソール|  
  
### <a name="role-and-role-services-windows-server-2012-or-windows-8-operating-systems"></a>ロールとロール サービス (Windows Server 2012 または Windows 8 オペレーティング システム)  
 Windows Server 2012 では、Microsoft 管理コンソール (MMC) にある **サーバー マネージャー**を使用して、 **Web サーバー (IIS)** ロールと、次に示す必要なロール サービスをインストールできます。  
  
> [!NOTE]  
>  Windows 8 オペレーティング システムでは、コントロール パネルの **[プログラムと機能]** を使用して、 **[Windows の機能]** ダイアログ ボックスに表示されるこれらのオプションを有効にします。  
  
||  
|-|  
|[インターネット インフォメーション サービス]<br /><br /> Web 管理ツール<br /><br /> IIS 管理コンソール<br /><br /> World Wide Web サービス<br /><br /> アプリケーション開発<br /><br /> .NET Extensibility 3.5<br /><br /> .NET Extensibility 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> ISAPI 拡張<br /><br /> ISAPI フィルター<br /><br /> HTTP 基本機能<br /><br /> 既定のドキュメント<br /><br /> ディレクトリの参照<br /><br /> HTTP エラー<br /><br /> 静的なコンテンツ<br /><br /> [注:WebDAV 発行はインストールしない]<br /><br /> 状態と診断<br /><br /> HTTP ログ<br /><br /> 要求の監視<br /><br /> パフォーマンス<br /><br /> 静的なコンテンツの圧縮<br /><br /> セキュリティ<br /><br /> 要求フィルター<br /><br /> [Windows 認証]|  
  
### <a name="features-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>機能 (Windows Server 2008 または Windows Server 2008 R2、Windows 7 オペレーティング システム)  
 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] または Windows Server 2008 R2 では、 **サーバー マネージャー** を使用して、次に示す必要な機能をインストールできます。  
  
> [!NOTE]  
>  [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] および Windows 7 オペレーティング システムでは、コントロール パネルの **[プログラムと機能]** を使用して、 **[Windows の機能]** ダイアログ ボックスに表示されるこれらのオプションを有効にします。  
  
||  
|-|  
|.NET Framework 3.0 の機能<br /><br /> WCF アクティブ化<br /><br /> HTTP アクティブ化<br /><br /> 非 HTTP アクティブ化<br /><br /> Windows プロセス アクティブ化サービス<br /><br /> プロセス モデル<br /><br /> .NET 環境<br /><br /> 構成 API|  
  
### <a name="features-windows-server-2012-or-windows-8-operating-systems"></a>機能 (Windows Server 2012 または Windows 8 オペレーティング システム)  
 Windows Server 2012 では、 **サーバー マネージャー** を使用して、次に示す必要な機能をインストールできます。  
  
> [!NOTE]  
>  Windows 8 オペレーティング システムでは、コントロール パネルの **[プログラムと機能]** を使用して、 **[Windows の機能]** ダイアログ ボックスに表示されるこれらのオプションを有効にします。  
  
||  
|-|  
|.NET Framework 3.5 (.NET 2.0 および 3.0 を含む)<br /><br /> .NET Framework 4.5 Advanced Services<br /><br /> ASP.NET 4.5<br /><br /> WCF サービス<br /><br /> HTTP のアクティブ化 [注:これが必要です。]<br /><br /> TCP ポート共有<br /><br /> Windows プロセス アクティブ化サービス<br /><br /> プロセス モデル<br /><br /> .NET 環境<br /><br /> 構成 API|  
  
### <a name="accounts-and-permissions"></a>アカウントと権限  
  
|型|説明|  
|----------|-----------------|  
|Windows アカウント|Windows のロール、ロール サービス、および機能を構成し、ローカル コンピューター上の IIS にあるアプリケーション プール、Web サイト、および Web アプリケーションを作成して管理する権限がある Windows アカウントを使用して Web サーバー コンピューターにログオンする必要があります。|  
|サービス アカウント|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] で [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]Web アプリケーションを作成するときは、アプリケーションが実行されるアプリケーション プールの ID を指定する必要があります。 このアカウントは、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースの作成時に指定したサービス アカウントと異なっていてもかまいません。<br /><br /> この ID はドメイン ユーザー アカウントである必要があり、データベースにアクセスするために [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースの mds_exec データベース ロールに追加されます。 詳細については、「[データベース ログイン、ユーザー、およびロール &#40;マスター データ サービス&#41;](../database-logins-users-and-roles-master-data-services.md)」を参照してください。 また、このアカウントは、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Windows グループ **MDS_ServiceAccounts** にも追加されます。このグループには、ファイル システムの一時コンパイル ディレクトリ **MDSTempDir** に対する権限が与えられています。 詳細については、「[フォルダーとファイルの権限 &#40;マスター データ サービス&#41;](../folder-and-file-permissions-master-data-services.md)」を参照してください。<br /><br /> サーバーのエラーを回避するには、アプリケーション プール アカウントに VIEW SERVER STATE 権限が必要です。 たとえば、MDS Validate Version コマンドはサーバー エラーで失敗します。 詳細については、「 [SQL Server 2012 および SQL Server 2014 で MDS Validate Version コマンドがサーバー エラーで失敗する](https://go.microsoft.com/fwlink/p/?LinkId=526304)」を参照してください。|  
  
## <a name="see-also"></a>関連項目  
 [マスター データ サービスのインストール](install-master-data-services.md)   
 [マスター データ マネージャー Web アプリケーションの作成 &#40;マスター データ サービス&#41;](create-a-master-data-manager-web-application-master-data-services.md)   
 [[Web の構成] ページ &#40;マスター データ サービス構成マネージャー&#41;](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  
