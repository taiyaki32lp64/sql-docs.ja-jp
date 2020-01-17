---
title: サブジェクト代替名を使用する Reporting Services の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ce458f9f-4b4f-4a58-aa75-9a90dda1e622
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 39cb8593351e97c47fff38ae2d1b6f2b326f49b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109741"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>サブジェクト代替名を使用するように Reporting Services を構成する
  このトピックでは、rsreportserver.config ファイルを変更し、Netsh.exe ツールを使用することによって、サブジェクト代替名 (SAN) を使用するように [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) を構成する方法について説明します。  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ネイティブ モード|  
  
 この手順は、レポート サービスの URL および Web サービス URL に適用されます。  
  
 SAN を使用するには、SSL 証明書がサーバーに登録され、署名され、秘密キーを保持している必要があります。 自己署名証明書は使用できません  
  
 SSL 証明書を使用するように、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の URL を構成できます。 通常、証明書にはサブジェクト名のみが記載されているため、SSL (Secure Sockets Layer) セッションに対して許可される URL は 1 つだけです。 SAN は、SSL サービスがリッスンでき、多数の URL 対して有効化され、SSL ポートを他のアプリケーションと共有できるようにするための証明書の追加フィールドです。 SAN は、 www.s2.com のようになります。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]のSSL 設定の詳細については、「 [ネイティブ モードのレポート サーバーでの SSL 接続の構成](security/configure-ssl-connections-on-a-native-mode-report-server.md)」を参照してください。  
  
### <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>サブジェクト代替名を Web サービス URL に使用するように SSRS を構成します。  
  
1.  Reporting Services 構成マネージャーを開始します。  
  
     詳細については、「 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../sql-server/install/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
2.  **[Web サービス URL]** ページで、SSL ポートおよび SSL 証明書を選択します。  
  
     ![Reporting Services 構成マネージャー](media/reportingservices-configurationmanager.png "Reporting Services 構成マネージャー")  
  
     構成マネージャーは、ポート用に SSL 証明書を登録します。  
  
3.  rsreportserver.config ファイルを開きます。  
  
     SSRS ネイティブ モードの場合、ファイルは、既定では、次のフォルダーにあります。  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  レポート サーバー Web サービス アプリケーションの URL セクションをコピーします。  
  
     たとえば、元の URL セクションを次に示します。  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     変更後の URL セクションを次に示します。  
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  rsreportserver.config ファイルを保存します。  
  
6.  管理者としてコマンド プロンプトを起動し、Netsh.exe ツールを実行します。  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  次のように入力して、http コンテキストに切り替えます。  
  
    ```  
    Netsh>http  
    ```  
  
8.  次のように入力して、既存の urlacl を表示します。  
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     次のようなエントリが表示されます。  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     urlacl は、予約された URL の DACL (任意のアクセス制御リスト) です。  
  
9. 次のように入力して、既存のエントリと同じユーザーおよび SDDL を持つ、サブジェクト代替名の新しいエントリを作成します。  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. Reporting Services 構成マネージャーの **[レポート サーバーの状態]** ページで、 **[停止]** をクリックしてから **[開始]** をクリックし、レポート サーバーを再起動します。  
  
## <a name="see-also"></a>関連項目  
 [RSReportServer 構成ファイル](report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
