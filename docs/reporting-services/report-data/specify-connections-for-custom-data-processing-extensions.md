---
title: カスタム データ処理拡張機能の接続を指定する | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- IDbConnection interface, connection strings
- impersonation [Reporting Services]
- IDbConnectionExtension interface, connection strings
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- data processing extensions [Reporting Services], connections
ms.assetid: 2cddc9ea-0e28-4350-80ae-332412908e47
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f346427ee41f8049caa050aa49eda393dd304566
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575489"
---
# <a name="specify-connections-for-custom-data-processing-extensions"></a>カスタム データ処理拡張機能の接続を指定する
  サード パーティ製のカスタム データ処理拡張機能をレポート サーバー上で作成または使用して、サポートされているデータ ソースのデータ処理能力を向上したり、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の既定のインストールで使用できないその他の種類のデータ ソースをサポートしたりできます。 接続の処理方法は実装によって異なります。 データ処理拡張機能に使用できる実装は次のとおりです。  
  
-   カスタム [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダー (DB2.NET、Oracle、ODP.NET、または Teradata データ ソースからデータへアクセスしている場合は、カスタム .NET データ プロバイダーを使用している可能性があります)  
  
-   <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> をサポートするカスタム データ処理拡張機能  
  
-   <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> をサポートするカスタム データ処理拡張機能  
  
> [!NOTE]  
>  カスタム データ処理拡張機能の実装方法はサード パーティ プロバイダーに問い合わせてください。  
  
## <a name="impersonation-and-custom-data-processing-extensions"></a>権限借用とカスタム データ処理拡張機能  
 権限借用を使用してカスタム データ処理拡張機能がデータ ソースへ接続する場合は、 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> または <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> のインターフェイスで Open メソッドを使用して要求を行う必要があります。 または、ユーザー ID オブジェクト (System.Security.Principal.WindowsIdentity) を格納後、他のデータ処理拡張機能 API でそのユーザー ID オブジェクトを再利用できます。  
  
 以前のリリースの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、すべてのカスタム データ処理拡張機能はユーザーの権限借用により呼び出されました。 このリリースでは、ユーザーの権限を借用している間に Open メソッドのみ呼び出されます。 統合セキュリティを必要とする既存のデータ処理拡張機能の場合は、Open メソッドを使用するように、またはユーザー ID オブジェクトを格納するようにコードを変更する必要があります。  
  
## <a name="connections-for-custom-net-framework-data-providers"></a>カスタム .NET Framework データ プロバイダーの接続  
 レポートを構成して特定のデータ ソースを使用する場合、データ ソースの種類、接続文字列、およびデータ ソースへのアクセスに使用される資格情報を決定するプロパティを設定します。 次の表では、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーでサポートされている資格情報の種類を示します。 レポート データ ソースのプロパティの設定の詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
|[資格情報]|接続|  
|-----------------|-----------------|  
|統合セキュリティ|データ プロバイダーがこの資格情報をサポートする場合は、Windows 統合セキュリティを使用できます。 現在のユーザーの資格情報を使用して要求が送信されます。<br /><br /> 接続文字列を定義する場合は、統合セキュリティを指定する引数を指定してください (たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ ソースへ接続する場合は接続文字列に **Integrated Security=SSPI** を含めます)。|  
|[Windows 認証]|データ プロバイダーがこの資格情報をサポートする場合は、Windows ドメイン ユーザー アカウントを使用できます。 レポート サーバーでは、データ処理拡張機能が呼び出される前にユーザー アカウントの権限が借用されます。<br /><br /> 接続文字列を定義する場合は、統合セキュリティを指定する引数を指定してください (たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ ソースへ接続する場合は接続文字列に **Integrated Security=SSPI** を含めます)。|  
|データベース資格情報|データベース認証は、カスタム .NET データ プロバイダー経由の接続に対してはサポートされていません。 すべての場合において、レポート サーバーは接続に失敗します。|  
|資格情報なし|カスタム .NET データ プロバイダーでは、資格情報なしのオプションを使用できます。 自動実行アカウントが指定されている場合、使用する資格情報は接続文字列によって決定されます。 レポート サーバーでは、自動実行アカウントの権限が借用され、接続が行われます。<br /><br /> 自動実行アカウントが定義されていない場合、レポート サーバーは接続に失敗します。 アカウントの定義の詳細については、「 [自動実行アカウントの構成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。|  
  
## <a name="connections-for-idbconnection"></a>IDbConnection の接続  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> のみサポートするカスタム データ処理拡張機能を使用する場合、次の方法で接続を指定する必要があります。  
  
1.  自動実行アカウントを構成する。 **IDbConnection**を使用する接続を行うためにはこのアカウントを構成する必要があります。 レポート サーバーでは、接続時にアカウントの権限が借用されます。  
  
2.  **[資格情報なし]** を使用するためにデータ ソース プロパティをレポート上に構成します。  
  
3.  データ ソースへの接続に使用した資格情報を接続文字列に指定します。  
  
 **IDbConnection**を使用する場合には、統合セキュリティ、Windows ユーザー アカウント、およびデータベース資格情報はサポートされません。 データ ソース接続にこれらのオプションを使用した場合、レポート サーバーは接続に失敗します。  
  
## <a name="connections-for-idbconnectionextension"></a>IDbConnectionExtension の接続  
 カスタム データ処理拡張機能を使用し、 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>がサポートされる場合、次の方法で接続を指定できます。  
  
|[資格情報]|接続|  
|-----------------|-----------------|  
|統合セキュリティ|データ プロバイダーがこの資格情報をサポートする場合は、 **IDbConnectionExtension**を使用するカスタム データ処理拡張機能を持つ Windows 統合セキュリティを使用できます。<br /><br /> 接続文字列を定義する場合は、統合セキュリティを指定する引数を指定してください (たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ ソースへ接続する場合は接続文字列に **Integrated Security=SSPI** を含めます)。|  
|[Windows 認証]|データ プロバイダーがこの資格情報をサポートする場合は、 **IDbConnectionExtension**を使用するカスタム データ処理拡張機能の Windows ドメイン ユーザー アカウントを使用できます。<br /><br /> レポート サーバーでは、データ処理拡張機能が呼び出される前にユーザー アカウントの権限が借用されます。 接続文字列を定義する場合は、統合セキュリティを指定する引数を指定してください (たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ ソースへ接続する場合は接続文字列に **Integrated Security=SSPI** を含めます)。|  
|データベース資格情報|データベース認証を使用して、 **IDbConnectionExtension**を使用するカスタム データ処理拡張機能の接続を構成できます。|  
|資格情報なし|自動実行アカウントが指定されている場合、使用する資格情報は接続文字列によって決定されます。<br /><br /> 自動実行アカウントが定義されていない場合、レポート サーバーは接続に失敗します。|  
  
## <a name="see-also"></a>参照  
 [自動実行アカウントの構成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [データ接続、データ ソース、および接続文字列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [データ処理拡張機能の実装](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [レポートのデータ ソースのプロパティを構成する](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
