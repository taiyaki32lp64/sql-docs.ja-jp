---
title: MSReportServer_ConfigurationSetting メンバー | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Members
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 134c115e48bd578f794ecce28d770ce955622f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65569162"
---
# <a name="msreportserverconfigurationsetting-members"></a>MSReportServer_ConfigurationSetting メンバー
  MSReportServer_ConfigurationSetting クラスには、次のプロパティとメソッドが含まれています。  
  
## <a name="public-properties"></a>パブリック プロパティ  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスとの通信にレポート サーバーが使用する接続プール サイズを返します。 読み取り専用です。|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに接続するためにレポート サーバーが使用するログイン アカウントを指定します。 読み取り専用です。|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|レポート サーバー データベースへのログインを失敗と判断するまでの待機時間を秒数で指定します。 読み取り専用です。|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|レポート サーバーが Window サービス アカウント、Windows ユーザー アカウント、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのいずれを使用してレポート サーバー データベースにアクセスするかを指定します。 読み取り専用です。|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を指定します。|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|コマンドが失敗またはタイムアウトするまでに経過する必要がある秒数を指定します。レポート サーバーは、レポートのデータ ソースではなく、レポート サーバー データベースに対する処理時間を計測します。|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|レポート サーバー データベースがインストールされるサーバーの名前を指定します。|  
|[InstallationID Property](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|特定のレポート サーバー インスタンスの一意な識別子を返します。|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|特定のコンピューターのレポート サーバー インスタンスの名前を指定します。|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|レポート サーバー インスタンスが初期化されているかどうかを示します。 読み取り専用です。|  
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
  
## <a name="public-methods"></a>パブリック メソッド  
  
|||  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)|インスタンスの暗号化キーをバックアップします。 暗号化キーは、パスワードを使用して暗号化されて格納されます。|  
|[CreateSSLCertificateBinding メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-createsslcertificatebinding.md)|SSL 証明書のバインドを作成します。|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptedinformation.md)|レポート サーバー データベースから暗号化された情報を削除します。|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptionkey.md)|レポート サーバー データベースから暗号化キーを削除します。|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)|レポート サーバー データベースの作成に使用できる SQL スクリプトを生成します。|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)|レポート サーバー データベースへのユーザー権限の付与に使用できる SQL スクリプトを生成します。|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)|レポート サーバー データベースのアップグレードに使用できる SQL スクリプトを生成します。|  
|[GetAdminSiteUrl メソッド &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getadminsiteurl.md)|サーバーの管理 Web サイトの絶対 URL を取得します。|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getdatabaseversiondisplayname.md)|指定したレポート サーバー データベースのバージョン文字列の表示名を取得します。|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-initializereportserver.md)|指定されたレポート サーバー インスタンスを初期化します。|  
|[ListInstalledSharePointVersions メソッド (WMI)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listinstalledsharepointversions.md)|レポート サーバーと同じコンピューターにインストールされた [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]、 or [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] のバージョンを表すトークンのセットを返します。|  
|[ListIPAddresses メソッド (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listipaddresses.md)|コンピューターの IP アドレスを一覧表示します。|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreportserversindatabase.md)|セキュリティで保護された情報にアクセスできるかどうかに関係なく、レポート サーバー データベースにあるレポート サーバーの一覧を返します。|  
|[ListReservedURLs メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreservedurls.md)|レポート サーバー上のすべてのアプリケーション用に予約されている URL を一覧表示します。|  
|[ListSSLCertificateBindings メソッド (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificatebindings.md)|HTTP.SYS に存在する SSL 証明書のバインドと rsreportserver.config から予測される SSL 証明書のバインドを一覧表示します。|  
|[ListSSLCertificate メソッド (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificates.md)|コンピューターにインストールされている SSL 証明書を一覧表示します。|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reencryptsecureinformation.md)|新しい暗号化キーを生成し、その新しいキーを使用してレポート サーバー データベース内のセキュリティで保護されたすべての情報を再度暗号化します。|  
|[RemoveSSLCertificateBindings メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removesslcertificatebinding.md)|SSL 証明書のバインドを削除します。|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeunattendedexecutionaccount.md)|レポート サーバー構成から自動実行用アカウント エントリを削除します。|  
|[RemoveURL メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeurl.md)|レポート サーバー用に予約されている URL を削除します。|  
|[ReserveURL メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)|指定したアプリケーションの URL 予約を追加します。|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-restoreencryptionkey.md)|指定した暗号化キーをレポート サーバー データベースに再適用します。|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaseconnection.md)|特定のレポート サーバー データベースへのレポート サーバー データベース接続を設定します。|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaselogontimeout.md)|レポート サーバー データベースのログオン試行に関する既定のタイムアウト値を指定します。|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabasequerytimeout.md)|レポート サーバー データベース接続に関する既定のタイムアウト値を指定します。|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setemailconfiguration.md)|レポート サーバーが電子メール送信に使用する電子メール配信拡張機能を構成します。|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)|レポート サーバーのセキュリティで保護された接続レベルを設定します。|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setservicestate.md)|レポート サーバーの Windows サービスおよび Web サービスを開始または停止します。|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setunattendedexecutionaccount.md)|レポートの自動実行に使用するアカウントを指定します。|  
|[SetVirtualDirectory メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md)|アプリケーションの仮想ディレクトリを設定します。|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setwindowsserviceidentity.md)|指定した Windows ユーザーとしてレポート サーバーの Windows サービスを実行し、レポート サーバーを運用できるファイル システム権限をこのアカウントに与えます。|  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting Class](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
