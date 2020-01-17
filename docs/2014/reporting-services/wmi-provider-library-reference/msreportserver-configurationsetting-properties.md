---
title: MSReportServer_ConfigurationSetting プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Properties
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c3937d888089f06435fece25e791b10ebbab785
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097326"
---
# <a name="msreportserverconfigurationsetting-properties"></a>MSReportServer_ConfigurationSetting プロパティ
  MSReportServer_ConfigurationSetting クラスは、レポート サーバー インスタンスのインストールおよび実行時のパラメーターを表します。 これらの設定は、RSReportServer.config 構成ファイルに格納されます。  
  
## <a name="public-properties"></a>パブリック プロパティ  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスとの通信にレポート サーバーが使用する接続プール サイズを返します。 読み取り専用。|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに接続するためにレポート サーバーが使用するログオン アカウントを指定します。 読み取り専用。|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|レポート サーバー データベースへのログインを失敗と判断するまでの待機時間を秒数で指定します。 読み取り専用。|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|レポート サーバーが Window サービス アカウント、Windows ユーザー アカウント、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのいずれを使用してレポート サーバー データベースにアクセスするかを指定します。 読み取り専用。|  
|[DatabaseName](configurationsetting-property-databasename.md)|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を指定します。|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|コマンドが失敗またはタイムアウトするまでに経過する必要がある秒数を指定します。レポート サーバーは、レポートのデータ ソースではなく、SQL Server カタログに対してプロセスの時刻設定をします。|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|レポート サーバー データベースがインストールされるサーバーの名前を指定します。|  
|[InstallationID Property](configurationsetting-property-installationid.md)|特定のレポート サーバー インスタンスの一意な識別子を返します。|  
|[InstanceName](configurationsetting-property-instancename.md)|特定のコンピューターのレポート サーバー インスタンスの名前を指定します。|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|レポート サーバー インスタンスが初期化されているかどうかを示します。  読み取り専用。|  
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
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
