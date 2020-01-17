---
title: MSReportServer_ConfigurationSetting メンバー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Members
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df662a1ecfe70b9a28eff3947dee4aa769ef2506
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097310"
---
# <a name="msreportserverconfigurationsetting-members"></a>MSReportServer_ConfigurationSetting メンバー
  MSReportServer_ConfigurationSetting クラスには、次のプロパティとメソッドが含まれています。  
  
## <a name="public-properties"></a>パブリック プロパティ  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスとの通信にレポート サーバーが使用する接続プール サイズを返します。 読み取り専用。|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに接続するためにレポート サーバーが使用するログイン アカウントを指定します。 読み取り専用。|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|レポート サーバー データベースへのログインを失敗と判断するまでの待機時間を秒数で指定します。 読み取り専用。|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|レポート サーバーが Window サービス アカウント、Windows ユーザー アカウント、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのいずれを使用してレポート サーバー データベースにアクセスするかを指定します。 読み取り専用。|  
|[DatabaseName](configurationsetting-property-databasename.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を指定します。|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|コマンドが失敗またはタイムアウトするまでに経過する必要がある秒数を指定します。レポート サーバーは、レポートのデータ ソースではなく、レポート サーバー データベースに対する処理時間を計測します。|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|レポート サーバー データベースがインストールされるサーバーの名前を指定します。|  
|[InstallationID Property](configurationsetting-property-installationid.md)|特定のレポート サーバー インスタンスの一意な識別子を返します。|  
|[InstanceName](configurationsetting-property-instancename.md)|特定のコンピューターのレポート サーバー インスタンスの名前を指定します。|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|レポート サーバー インスタンスが初期化されているかどうかを示します。 読み取り専用。|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|レポート サーバーが SharePoint 統合モード用に構成されているかどうかを示します。|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|レポート サーバー Web サービスが有効かどうかを示します。 読み取り専用。|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|レポート サーバー Windows サービスが有効かどうかを示します。 読み取り専用。|  
|[MachineAccountIdentity プロパティ &#40;WMI&#41;](configurationsetting-property-machineaccountidentity.md)|レポート サーバーがインストールされているコンピューターのコンピューター アカウント ID を取得します。|  
|[PathName](configurationsetting-property-pathname.md)|レポート サーバー インスタンスのインストール パスを指定します。|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|RSReportServer.config ファイルに指定された、セキュリティで保護された接続レベルを返します。|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|レポート サーバーからの電子メール送信に使用するアドレスを取得します。 読み取り専用。|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|電子メール構成の SendUsing プロパティを TRUE に設定するかどうかを示します。|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|RSReportServer.config ファイルから SMTP サーバー プロパティを取得します。 読み取り専用。|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|レポートを自動実行するときにレポート サーバーで権限を借用するログイン ユーザー アカウントを指定します。 読み取り専用。|  
|[バージョン](configurationsetting-property-version.md)|レポート サーバーのバージョンを返します。|  
|[VirtualDirectoryReportManager プロパティ &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|レポート マネージャー アプリケーションの仮想ディレクトリを返します。|  
|[VirtualDirectoryReportServer プロパティ &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|レポート サーバー Web サービス アプリケーションの仮想ディレクトリを返します。|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|レポート サーバー Windows サービスが実際に実行されている ID を返します。 読み取り専用。|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|レポート サーバー Windows サービスが実行するように最後に構成された ID を返します。 読み取り専用。|  
  
## <a name="public-methods"></a>パブリック メソッド  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|インスタンスの暗号化キーをバックアップします。 暗号化キーは、パスワードを使用して暗号化されて格納されます。|  
|[CreateSSLCertificateBinding メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-createsslcertificatebinding.md)|SSL 証明書のバインドを作成します。|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|レポート サーバー データベースから暗号化された情報を削除します。|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|レポート サーバー データベースから暗号化キーを削除します。|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|レポート サーバー データベースの作成に使用できる SQL スクリプトを生成します。|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|レポート サーバー データベースへのユーザー権限の付与に使用できる SQL スクリプトを生成します。|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|レポート サーバー データベースのアップグレードに使用できる SQL スクリプトを生成します。|  
|[GetAdminSiteUrl メソッド &#40;WMI&#41;](configurationsetting-method-getadminsiteurl.md)|サーバーの管理 Web サイトの絶対 URL を取得します。|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|指定したレポート サーバー データベースのバージョン文字列の表示名を取得します。|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|指定されたレポート サーバー インスタンスを初期化します。|  
|[ListInstalledSharePointVersions メソッド (WMI)](configurationsetting-method-listinstalledsharepointversions.md)|レポート サーバーと同じコンピューターにインストールされた [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]、 or [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] のバージョンを表すトークンのセットを返します。|  
|[ListIPAddresses メソッド (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listipaddresses.md)|コンピューターの IP アドレスを一覧表示します。|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|セキュリティで保護された情報にアクセスできるかどうかに関係なく、レポート サーバー データベースにあるレポート サーバーの一覧を返します。|  
|[ListReservedURLs メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listreservedurls.md)|レポート サーバー上のすべてのアプリケーション用に予約されている URL を一覧表示します。|  
|[ListSSLCertificateBindings メソッド (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listsslcertificatebindings.md)|HTTP.SYS に存在する SSL 証明書のバインドと rsreportserver.config から予測される SSL 証明書のバインドを一覧表示します。|  
|[ListSSLCertificate メソッド (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listsslcertificates.md)|コンピューターにインストールされている SSL 証明書を一覧表示します。|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|新しい暗号化キーを生成し、その新しいキーを使用してレポート サーバー データベース内のセキュリティで保護されたすべての情報を再度暗号化します。|  
|[RemoveSSLCertificateBindings メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removesslcertificatebinding.md)|SSL 証明書のバインドを削除します。|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|レポート サーバー構成から自動実行用アカウント エントリを削除します。|  
|[RemoveURL メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removeurl.md)|レポート サーバー用に予約されている URL を削除します。|  
|[ReserveURL メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-reserveurl.md)|指定したアプリケーションの URL 予約を追加します。|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|指定した暗号化キーをレポート サーバー データベースに再適用します。|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|特定のレポート サーバー データベースへのレポート サーバー データベース接続を設定します。|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|レポート サーバー データベースのログオン試行に関する既定のタイムアウト値を指定します。|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|レポート サーバー データベース接続に関する既定のタイムアウト値を指定します。|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|レポート サーバーが電子メール送信に使用する電子メール配信拡張機能を構成します。|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|レポート サーバーのセキュリティで保護された接続レベルを設定します。|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|レポート サーバーの Windows サービスおよび Web サービスを開始または停止します。|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|レポートの自動実行に使用するアカウントを指定します。|  
|[SetVirtualDirectory メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md)|アプリケーションの仮想ディレクトリを設定します。|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|指定した Windows ユーザーとしてレポート サーバーの Windows サービスを実行し、レポート サーバーを運用できるファイル システム権限をこのアカウントに与えます。|  
  
## <a name="see-also"></a>関連項目  
 [MSReportServer_ConfigurationSetting Class](msreportserver-configurationsetting-class.md)  
  
  
