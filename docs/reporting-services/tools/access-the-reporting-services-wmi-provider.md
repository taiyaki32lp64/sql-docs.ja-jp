---
title: Reporting Services WMI プロバイダーへのアクセス | Microsoft Docs
ms.date: 11/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
apiname:
- Reporting Services WMI Provider
apilocation:
- reportingservices.mof
helpviewer_keywords:
- WMI provider [Reporting Services]
- programming [Reporting Services]
ms.assetid: 22cfbeb8-4ea3-4182-8f54-3341c771e87b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bbce09bb5c76d29bf56defb3c5403665e5226558
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576759"
---
# <a name="access-the-reporting-services-wmi-provider"></a>Reporting Services WMI プロバイダーへのアクセス
  Reporting Services WMI プロバイダーは、ネイティブ モードのレポート サーバー インスタンスの管理に使用できる 2 つの WMI クラスを、スクリプトを通じて公開します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] リリース以降では、WMI プロバイダーはネイティブ モードのレポート サーバーに対してのみサポートされています。 SharePoint モードのレポート サーバーは、SharePoint サーバーの全体管理ページおよび PowerShell スクリプトを使用して管理できます。  
  
|クラス|Namespace|[説明]|  
|-----------|---------------|-----------------|  
|MSReportServer_Instance|root\Microsoft\SqlServer\ReportServer\RS_ *\<EncodedInstanceName>* \v13|インストールされているレポート サーバーに接続するための基本情報をクライアントに提供します。|  
|MSReportServer_ConfigurationSetting|root\Microsoft\SqlServer\ReportServer\RS_ *\<EncodedInstanceName>* \v13\Admin|レポート サーバー インスタンスのインストール パラメーターとランタイム パラメーターを表します。 これらのパラメーターはレポート サーバーの構成ファイルに格納されています。<br /><br /> **\*\* 重要 \*\*** このクラスは管理者権限でのみアクセス可能です。|  
  
 上記のクラスの各インスタンスは、レポート サーバー インスタンスごとに作成されます。 レポート サーバーによって公開されている WMI オブジェクト (.NET Framework 自体によって公開されている WMI プログラミング インターフェイスを含む) へは、Microsoft またはサード パーティの任意のツールを使用してアクセスできます。 このトピックでは、PowerShell コマンド [Get-WmiObject](https://technet.microsoft.com/library/dd315295.aspx)を使用した、WMI クラスのインスタンスに対するアクセス方法と使用方法について説明します。  
  
## <a name="determine-the-instance-name-in-the-namespace-string"></a>名前空間文字列内のインスタンス名の確認  
 Reporting Services WMI クラスの名前空間パスに含まれるインスタンス名は、名前付き Reporting Services インスタンスのインストール時に指定したインスタンス名のエンコードです。 つまり、インスタンス名に含まれる特殊文字はエンコードされます。 たとえば、アンダースコア (_) は "_5f" としてエンコードされるので、"My_Instance" のインスタンス名は WMI 名前空間パス内では "My_5fInstance" としてエンコードされます。  
  
 使用しているレポート サーバー インスタンスについて、WMI 名前空間パス内でのエンコード後のインスタンス名の一覧を表示するには、次の PowerShell コマンドを使用します。  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace root\Microsoft\SqlServer\ReportServer  -class __Namespace -ComputerName hostname | select Name  
```  
  
## <a name="access-the-wmi-classes-using-powershell"></a>PowerShell を使用した WMI クラスへのアクセス  
 WMI クラスにアクセスするには、次のコマンドを実行します。  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace <namespacename> -class <classname> -ComputerName <hostname>  
```  
  
 たとえば、ホスト myrshost の既定のレポート サーバー インスタンス上で MSReportServer_ConfigurationSetting クラスにアクセスするには、次のコマンドを実行します。 このコマンドを正常に実行するには、既定のレポート サーバー インスタンスが myrshost 上にインストールされている必要があります。  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERER\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost  
```  
  
 このコマンド構文は、すべてのクラス プロパティ名と値を出力します。 既定のレポート サーバー インスタンス (RS_MSSQLSERVER) の名前空間内のクラスにアクセスしている場合でも、MSReportServer_ConfigurationSetting クラスのすべてのインスタンスが返されます。 たとえば、myrshost が、既定のレポート サーバー インスタンスと、SHAREPOINT という名前付きレポート サーバー インスタンスを使用してインストールされている場合、このコマンドは、それら両方のレポート サーバー インスタンスのプロパティ名と値を出力します。  
  
 複数のインスタンスが返される場合、特定のクラス インスタンスが返されるようにするには、-Filter パラメーターを使用して、固有の値 (InstanceName など) を持つプロパティで結果をフィルター処理します。 たとえば、既定のレポート サーバー インスタンスの WMI オブジェクトのみを返すには、次のコマンドを使用します。  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='MSSQLSERVER'"  
```  
  
## <a name="query-the-available-methods-and-properties"></a>使用可能なメソッドとプロパティの照会  
 特定の Reporting Services WMI クラスで使用できるメソッドとプロパティを確認するには、Get-WmiObject から Get-Member へと結果をパイプします。 例:  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost | Get-Member  
```  
  
## <a name="use-a-wmi-method-or-property"></a>WMI のメソッドまたはプロパティの使用  
 Reporting Services クラスに対する WMI オブジェクトを用意し、使用可能なメソッドとプロパティを確認したら、それらのメソッドとプロパティを使用できます。 たとえば、SHAREPOINT という名前付きレポート サーバー インスタンスを SharePoint 統合モードで作成した場合は、次のコマンド シーケンスを使用して、SharePoint サーバーの全体管理サイトの URL を取得できます。  
  
```  
PS C:\windows\system32> $rsconfig = Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='SHAREPOINT'"  
PS C:\windows\system32> $rsconfig.GetAdminSiteUrl()  
  
```  
  
## <a name="see-also"></a>参照  
 [Reporting Services WMI プロバイダー ライブラリ リファレンス (SSRS)](../../reporting-services/wmi-provider-library-reference/reporting-services-wmi-provider-library-reference-ssrs.md)   
 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
