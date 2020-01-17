---
title: Reporting Services の既定の配信拡張機能を変更する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], default delivery extension
ms.assetid: 5f6fee72-01bf-4f6c-85d2-7863c46c136b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e37dcf69a09d92236e0b8f4f97cb99541f1c7532
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783253"
---
# <a name="change-the-default-reporting-services-delivery-extension"></a>Reporting Services の既定の配信拡張機能を変更する
  サブスクリプション定義ページの [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] [配信者] **リストに表示される既定の配信拡張機能は** の構成設定で変更できます。 たとえば、ユーザーが新しいサブスクリプションを作成したときに電子メール配信ではなくファイル共有配信が既定で選択されるように構成を変更することができます。 また、ユーザー インターフェイスにおける配信拡張機能の表示順を変更することもできます。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ネイティブ モード | [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint モード  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] には、電子メールの配信拡張機能と Windows ファイル共有の配信拡張機能があります。 カスタム配信をサポートするため、独自の拡張機能またはサード パーティの拡張機能を配置している場合は、これら以外の配信拡張機能もレポート サーバーに含まれている可能性があります。 配信拡張機能を使用できるかどうかは、配信拡張機能がレポート サーバーに配置されているかどうかによって決まります。  
  
## <a name="default-native-mode-report-server-configuration"></a>ネイティブ モードのレポート サーバーの既定の構成  
 レポート マネージャーの **[配信者]** リストの配信拡張機能は、 **RSReportServer.config** ファイルの配信拡張機能のエントリ順に基づいて表示されます。 たとえば次の画像を見ると、電子メールが一覧の先頭に表示され、既定で選択状態になっています。  
  
 ![配信拡張機能の既定の一覧](../media/ssrs-default-delivery.png "配信拡張機能の既定の一覧")  
  
 以下に示すコードは、 **RSReportServer.config** の既定のセクションです。既定の配信拡張機能とレポート マネージャーにおける表示順がこのセクションで制御されます。 このファイルで電子メールが先に記述され、なおかつ既定として設定されていることに注目してください。  
  
```xml
<DeliveryUI>  
     <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
          <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
               <Configuration>  
               <RSEmailDPConfiguration>  
                    <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
               </RSEmailDPConfiguration>  
               </Configuration>  
     </Extension>  
     <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>  
</DeliveryUI>  
```  
  
#### <a name="configure-file-share-delivery-as-the-default-delivery-extension-in-report-manager"></a>レポート マネージャーでファイル共有配信を既定の配信拡張機能として構成する  
  
1.  ファイル共有配信が一覧の先頭に、既定の選択肢として表示されるように、この手順の各段階で構成を変更します。  
  
     テキスト エディターで RSReportServer.config ファイルを開きます。 構成ファイルの詳細については、「 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)」を参照してください。 以下の画像は、構成変更後の UI を示しています。  
  
     ![配信拡張機能の変更された一覧](../media/ssrs-modified-delivery.png "配信拡張機能の変更された一覧")  
  
2.  DeliveryUI セクションを以下の例のように変更します。主な変更点は次のとおりです。  
  
    1.  FileShare 拡張機能を電子メール拡張機能の前に移動。 レポート マネージャーにおける配信拡張機能の表示順が変更されます。  
  
    2.  ファイル共有拡張機能に DefaultExtension タグ `<DefaultDeliveryExtension>True</DefaultDeliveryExtension>` と拡張機能の終了タグ `</Extension>`を追加。  
  
    3.  既定としての電子メール拡張機能の構成を解除。 `<DefaultDeliveryExtension>False</DefaultDeliveryExtension>`  
  
    ```  
    <DeliveryUI>  
         <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider">  
              <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
         </Extension>  
         <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
         <DefaultDeliveryExtension>False</DefaultDeliveryExtension>  
         <Configuration>  
              <RSEmailDPConfiguration>  
                   <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
              </RSEmailDPConfiguration>  
         </Configuration>  
         </Extension>  
    </DeliveryUI>  
    ```  
  
3.  構成ファイルを保存します。  
  
4.  数分するとレポート サーバーに構成ファイルが再読み込みされ、新しい設定が反映されます。 構成ファイルを強制的に読み込ませるには、レポート サーバー サービスを再起動してください。  
  
     構成が読み取られると、次のイベントが Windows イベント ログに書き込まれます。  
  
     **イベント ID:** 109  
  
     **ソース:** Report Server Windows Service (インスタンス名)  
  
     RSReportServer.config ファイルが変更されました。  
  
## <a name="sharepoint-mode-report-servers"></a>SharePoint モードのレポート サーバー  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint モードでは、拡張機能の情報が、RsrReportServer.config ファイルにではなく SharePoint Service アプリケーションのデータベースに保存されます。 SharePoint モードの配信拡張機能の構成は PowerShell を使って変更することになります。  
  
#### <a name="configure-the-default-delivery-extension"></a>既定の配信拡張機能の構成  
  
1.  **[SharePoint 管理シェル]** を開きます。  
  
2.  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サービス アプリケーションの名前が既にわかっている場合、この手順は省略してかまいません。 次の PowerShell コマンドを使用して、SharePoint ファーム内の [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サービス アプリケーションを一覧表示します。  
  
    ```powershell
    Get-SPRSServiceApplication | Format-List *  
    ```  
  
3.  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サービス アプリケーション "ssrsapp" に使用されている現在の既定の配信拡張機能を次の PowerShell コードで確認します。  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -Like "ssrsapp*"};
    Get-SPRSExtension -Identity $app | Where {$_.ServerDirectivesXML -Like "<DefaultDelivery*"} | Format-List *
    ```  
  
## <a name="see-also"></a>参照  
 [Rsreportserver 構成ファイル](../report-server/rsreportserver-config-configuration-file.md)   
 [Rsreportserver 構成ファイル](../report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services でのファイル共有の配信](file-share-delivery-in-reporting-services.md)   
 [Reporting Services の電子メール配信](e-mail-delivery-in-reporting-services.md)   
 [電子メール配信&#40;SSRS 用にレポートサーバーを構成する Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
