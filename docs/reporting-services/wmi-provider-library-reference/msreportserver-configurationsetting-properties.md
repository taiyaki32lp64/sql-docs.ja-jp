---
title: MSReportServer_ConfigurationSetting プロパティ | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Properties
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 634c5065730ea58905f89ac0454cdda53552a126
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65569097"
---
# <a name="msreportserverconfigurationsetting-properties"></a>MSReportServer_ConfigurationSetting プロパティ
  MSReportServer_ConfigurationSetting クラスは、レポート サーバー インスタンスのインストールおよび実行時のパラメーターを表します。 これらの設定は、RSReportServer.config 構成ファイルに格納されます。  
  
## <a name="public-properties"></a>パブリック プロパティ  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスとの通信にレポート サーバーが使用する接続プール サイズを返します。 読み取り専用です。|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに接続するためにレポート サーバーが使用するログオン アカウントを指定します。 読み取り専用です。|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|レポート サーバー データベースへのログインを失敗と判断するまでの待機時間を秒数で指定します。 読み取り専用です。|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|レポート サーバーが Window サービス アカウント、Windows ユーザー アカウント、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのいずれを使用してレポート サーバー データベースにアクセスするかを指定します。 読み取り専用です。|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を指定します。|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|コマンドが失敗またはタイムアウトするまでに経過する必要がある秒数を指定します。レポート サーバーは、レポートのデータ ソースではなく、SQL Server カタログに対してプロセスの時刻設定をします。|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|レポート サーバー データベースがインストールされるサーバーの名前を指定します。|  
|[InstallationID Property](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|特定のレポート サーバー インスタンスの一意な識別子を返します。|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|特定のコンピューターのレポート サーバー インスタンスの名前を指定します。|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|レポート サーバー インスタンスが初期化されているかどうかを示します。  読み取り専用です。|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-issharepointintegrated.md)|レポート サーバーが SharePoint 統合モード用に構成されているかどうかを示します。|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswebserviceenabled.md)|レポート サーバー Web サービスが有効かどうかを示します。 読み取り専用です。|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswindowsserviceenabled.md)|レポート サーバー Windows サービスが有効かどうかを示します。 読み取り専用です。|  
|[MachineAccountIdentity プロパティ &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-machineaccountidentity.md)|レポート サーバーがインストールされているコンピューターのコンピューター アカウント ID を取得します。|  
|[PathName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-pathname.md)|レポート サーバー インスタンスのインストール パスを指定します。|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-secureconnectionlevel.md)|RSReportServer.config ファイルに指定された、セキュリティで保護された接続レベルを返します。|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-senderemailaddress.md)|レポート サーバーからの電子メール送信に使用するアドレスを取得します。 読み取り専用です。|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-sendusingsmtpserver.md)|電子メール構成の SendUsing プロパティを TRUE に設定するかどうかを示します。|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-smtpserver.md)|RSReportServer.config ファイルから SMTP サーバー プロパティを取得します。 読み取り専用です。|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-unattendedexecutionaccount.md)|レポートを自動実行するときにレポート サーバーで権限を借用するログイン ユーザー アカウントを指定します。 読み取り専用です。|  
|[バージョン](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-version.md)|レポート サーバーのバージョンを返します。|  
|[VirtualDirectoryReportManager プロパティ &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportmanager.md)|レポート マネージャー アプリケーションの仮想ディレクトリを返します。|  
|[VirtualDirectoryReportServer プロパティ &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportserver.md)|レポート サーバー Web サービス アプリケーションの仮想ディレクトリを返します。|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-windowsserviceidentityactual.md)|レポート サーバー Windows サービスが実際に実行されている ID を返します。 読み取り専用です。|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|レポート サーバー Windows サービスが実行するように最後に構成された ID を返します。 読み取り専用です。|  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  

  
