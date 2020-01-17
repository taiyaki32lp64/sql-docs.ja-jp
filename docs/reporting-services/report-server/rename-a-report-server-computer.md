---
title: レポート サーバー コンピューターの名前の変更 | Microsoft Docs
ms.date: 06/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- renaming report servers
ms.assetid: 82fc4ba2-291a-4939-a025-271b8d687c54
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3fe381daf1b89d76d9282f2c1a54c3940a3ffbe
ms.sourcegitcommit: 3f2936e727cf8e63f38e5f77b33442993ee99890
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2019
ms.locfileid: "67314043"
---
# <a name="rename-a-report-server-computer"></a>レポート サーバー コンピューターの名前の変更
  コンピューターの名前を変更すると、同じコンピューター上に存在する Web サーバーおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前が対応して変更されます。 場合によっては、コンピューター名を変更した後に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] にアクセスできなくなることがあります。 コンピューター名を変更した後にレポート サーバーを再構成するには、この記事で説明する手順を使用します。  
  
## <a name="renaming-a-sql-server-database-engine"></a>SQL Server データベース エンジンの名前の変更  
 レポート サーバー データベースを実行する  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] インスタンスの名前を変更する場合は、次の手順を実行します。  
  
1.  Reporting Services 構成ツールを起動し、名前が変更されたサーバー上のレポート サーバー データベースを使用するレポート サーバーに接続します。  
  
2.  [データベースのセットアップ] ページを開きます。  
  
3.  **[サーバー名]** で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前を入力または選択し、 **[接続]** をクリックします。  
  
4.  **[適用]** をクリックします。  
  
 レポート サーバーがローカルの [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスを使用している場合は、 *(local)* または *(local)\instancename* を使用して、サーバーを指定できます。 *(local)* を使用してサーバーを参照する場合は、サーバーの名前を変更しても、接続は引き続き機能します。 リモート サーバーを使用している場合や、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] がサーバー名を使用して構成されている場合は、サーバー名を変更するたびに、データベース接続情報を更新する必要があります。  
  
## <a name="renaming-a-report-server-computer"></a>レポート サーバー コンピューターの名前の変更  
 レポート サーバーを実行するコンピューターの名前を変更する場合は、次の手順を実行します。  
  
1.  テキスト エディターで RSReportServer.config を開き、新しいサーバー名を反映するように **UrlRoot** 設定を変更します。 **UrlRoot** 設定は、レポート サーバーに格納されているアイテムへのアクセスに使用する URL を構成するために、配信拡張機能によって使用されます。 レポート サーバーの URL アドレスを変更するには、 **UrlRoot** 設定を更新し、サブスクリプションによってレポートが引き続き適切に配信されるようにする必要があります。  
  
2.  同じファイルで、 **ReportServerUrl** が設定されている場合は、新しいサーバー名を反映するようにこの設定を変更します。 この設定はすべてのインストールで使用されているわけではありません。 この設定が空の場合は、何もしません。  
  
    > [!NOTE]  
    >  企業ネットワークで Windows Internet Naming Service (WINS) を使用している場合は、レポート サーバーと Web ポータルを以前の名前でしばらく利用できることがあります。 WINS は、サービスを提供する各コンピューターに IP アドレスをマップします。 名前を変更したコンピューターの IP アドレスが WINS により更新された後は、古いコンピューター名を使用してレポート サーバーまたは Web ポータルにアクセスすることはできなくなります。  
  
## <a name="see-also"></a>参照  
 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Start and Stop the Report Server Service](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [rsconfig ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)  
  