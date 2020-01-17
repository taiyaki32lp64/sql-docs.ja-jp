---
title: Reporting Services サービス アプリケーションの電子メールの構成 | Microsoft Docs
ms.date: 05/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1025ea1de1e349e640b285174ffab694f791fd21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68221644"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application"></a>Reporting Services サービス アプリケーションの電子メールの構成

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ警告機能は、電子メール メッセージで警告を送信します。 電子メールを送信するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを構成して、このサービス アプリケーションの電子メール配信拡張機能を変更しなければならない場合があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプション機能の電子メール配信拡張機能を使用する場合、電子メールの設定も必要です。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
### <a name="to-configure-e-mail-for-the-shared-service"></a>共有サービスの電子メールを構成するには  
  
1.  SharePoint の全体管理で **[アプリケーション管理]** をクリックします。  
  
2.  **[サービス アプリケーション]** グループで、 **[サービス アプリケーションの管理]** をクリックします。  
  
3.  **[名前]** ボックスの一覧で、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの名前をクリックします。  
  
4.  **[Reporting Services アプリケーションの管理]** ページの **[電子メールの設定]** をクリックします。  
  
5.  **[SMTP サーバーの使用]** を選択します。  
  
6.  **[送信 SMTP サーバー]** ボックスに、SMTP サーバーの名前を入力します。  
  
7.  **[差出人アドレス]** ボックスに、電子メール アドレスを入力します。  
  
     このアドレスはすべての警告電子メール メッセージの送信元になります。  
  
     **[差出人アドレス]** に指定するユーザーのアカウントは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションのアプリケーション プールを構成するときに指定した管理アカウントである必要があります。 権限がある場合、SharePoint サーバーの全体管理の [サービス アカウント] ページで既存の管理アカウントの一覧を表示できます。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="ntlm-authentication"></a>NTLM 認証  
  
1.  NTLM 認証を必要とする電子メール環境で匿名アクセスを許可しない場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの電子メール配信拡張機能の構成を変更する必要があります。 たとえば、 **[サブスクリプションの管理]** ページ サブスクリプションの **[最終結果]** に次のメッセージが表示される場合があります。  
  
    -   電子メールを送信できません: SMTP サーバーにセキュリティで保護された接続が必要であるか、またはクライアントが認証されていません。 サーバーの応答があった: 5.7.1 にクライアントが非 authenticatedMail は再送信されません。  
  
     **SMTPAuthenticate** の値を "2" に変更します。 この値はユーザー インターフェイスから変更することはできません。 次の PowerShell スクリプトの例では、"SSRS_TESTAPPLICATION" という名前のサービス アプリケーションについて、レポート サーバーの電子メール配信拡張機能の構成全体を更新します。 スクリプトに示されているノードの一部は、[差出人アドレス] などのユーザー インターフェイスからも設定できます。  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
    $emailXml = [xml]$emailCfg   
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = "your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = "your FROM email address"  
    Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  サービス アプリケーションの名前を確認する必要がある場合は、 **Get-SPRSServiceApplication コマンドレット**を実行します。  
  
    ```  
    get-sprsserviceapplication  
    ```  
  
3.  次の例では、"SSRS_TESTAPPLICATION" という名前のサービス アプリケーションについて、電子メール拡張機能の現在の値を返します。  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
    ```  
  
4.  次の例では、"SSRS_TESTAPPLICATION" という名前のサービス アプリケーションについて、電子メール拡張機能の現在の値を使用して "emailconfig.txt" という名前の新規ファイルを作成します。  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml | out-file c:\emailconfig.txt  
    ```  
  
  
その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
