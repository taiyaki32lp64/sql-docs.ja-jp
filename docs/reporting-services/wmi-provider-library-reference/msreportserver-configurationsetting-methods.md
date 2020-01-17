---
title: MSReportServer_ConfigurationSetting メソッド | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Methods
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b7d8110af1c3633e5e5fcc2a4e78ac3e70cc10c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65569193"
---
# <a name="msreportserverconfigurationsetting-methods"></a>MSReportServer_ConfigurationSetting メソッド
  レポート サーバー WMI プロバイダーの MSReportServer_ConfigurationSetting クラスには、次のパブリック メソッドがあります。  
  
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
|[ListInstalledSharePointVersions メソッド &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listinstalledsharepointversions.md)|レポート サーバーと同じコンピューターにインストールされた Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]、 or [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] のバージョンを表すトークンのセットを返します。|  
|[ListIPAddresses メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listipaddresses.md)|コンピューターの IP アドレスを一覧表示します。|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreportserversindatabase.md)|セキュリティで保護された情報にアクセスできるかどうかに関係なく、レポート サーバー データベースにあるレポート サーバーの一覧を返します。|  
|[ListReservedURLs メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreservedurls.md)|レポート サーバー上のすべてのアプリケーション用に予約されている URL を一覧表示します。|  
|[ListSSLCertificateBindings メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificatebindings.md)|HTTP.SYS に存在する SSL 証明書のバインドと RSReportServer.config から予測される SSL 証明書のバインドを一覧表示します。|  
|[ListSSLCertificate メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificates.md)|コンピューターにインストールされている SSL 証明書を一覧表示します。|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reencryptsecureinformation.md)|新しい暗号化キーを生成し、その新しいキーを使用してレポート サーバー データベース内のセキュリティで保護されたすべての情報を再度暗号化します。|  
|[RemoveSSLCertificateBindings メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removesslcertificatebinding.md)|SSL 証明書のバインドを削除します。|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeunattendedexecutionaccount.md)|レポート サーバー構成から自動実行用アカウント エントリを削除します。|  
|[RemoveURL メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeurl.md)|レポート サーバー用に予約されている URL を削除します。|  
|[ReserveURL メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)|指定したアプリケーションの URL 予約を追加します。|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-restoreencryptionkey.md)|指定した暗号化キーをレポート サーバー データベースに再適用します。|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaseconnection.md)|特定のレポート サーバー データベースへのレポート サーバー データベース接続を設定します。|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaselogontimeout.md)|レポート サーバー データベースのログオン試行に関する既定のタイムアウト値を指定します。|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabasequerytimeout.md)|レポート サーバー データベース クエリの既定のタイムアウト値を指定します。|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setemailconfiguration.md)|レポート サーバーが電子メール送信に使用する電子メール配信拡張機能を構成します。|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)|レポート サーバーのセキュリティで保護された接続レベルを設定します。|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setservicestate.md)|レポート サーバー サービスを開始または停止します。|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setunattendedexecutionaccount.md)|レポートの自動実行に使用するアカウントを指定します。|  
|[SetVirtualDirectory メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md)|アプリケーションの仮想ディレクトリを設定します。|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setwindowsserviceidentity.md)|指定した Windows ユーザーとしてレポート サーバー サービスを実行し、レポート サーバーを運用するためのファイル システム権限をこのアカウントに与えます。|  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting Class](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
