---
title: Reporting Services サービスアプリケーションの電子メールの構成 (SharePoint 2010 および SharePoint 2013) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6caa06af68eddfd85cb4f19ab2cfb8dd41bbdd95
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798108"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application-sharepoint-2010-and-sharepoint-2013"></a>Reporting Services サービス アプリケーションの電子メールの構成 (SharePoint 2010 および SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ警告機能は、電子メール メッセージで警告を送信します。 電子メールを送信するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを構成して、このサービス アプリケーションの電子メール配信拡張機能を変更しなければならない場合があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプション機能の電子メール配信拡張機能を使用する場合、電子メールの設定も必要です。  
  
||  
|-|  
|sharepoint モード&#124;の sharepoint 2010 および sharepoint 2013 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[applies](../../includes/applies-md.md)] ます。|  
  
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
  
1.  NTLM 認証を必要とする電子メール環境で匿名アクセスを許可しない場合、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの電子メール配信拡張機能の構成を変更する必要があります。 **SMTPAuthenticate** の値を "2" に変更します。 この値はユーザー インターフェイスから変更することはできません。 次の PowerShell スクリプトの例では、"SSRS_TESTAPPLICATION" という名前のサービス アプリケーションについて、レポート サーバーの電子メール配信拡張機能の構成全体を更新します。 スクリプトに示されているノードの一部は、[差出人アドレス] などのユーザー インターフェイスからも設定できます。  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml
    $emailXml = [xml]$emailCfg
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = "your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = "your FROM email address"  
    Set-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  サービスアプリケーションの名前を確認する必要がある場合は、 **get-sprsserviceapplication**コマンドレットを実行します。  
  
    ```powershell
    Get-SPRSServiceApplication  
    ```  
  
3.  次の例では、"SSRS_TESTAPPLICATION" という名前のサービス アプリケーションについて、電子メール拡張機能の現在の値を返します。  
  
    ```powershell
    $app = get-sprsserviceapplication | Where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml  
    ```  
  
4.  次の例では、"SSRS_TESTAPPLICATION" という名前のサービス アプリケーションについて、電子メール拡張機能の現在の値を使用して "emailconfig.txt" という名前の新規ファイルを作成します。  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | Select -ExpandProperty ConfigurationXml | Out-File c:\emailconfig.txt  
    ```
