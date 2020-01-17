---
title: Reporting Services の構成ファイル (RSreportserver.config) の変更 | Microsoft Docs
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 958ef51f-2699-4cb2-a92e-3b4322e36a30
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e97dff2a6d08207d95b28ce2f9a0cedafd9b6fff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581128"
---
# <a name="modify-a-reporting-services-configuration-file-rsreportserverconfig"></a>Modify a Reporting Services Configuration File (RSreportserver.config)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、一連の構成ファイルにアプリケーション設定を格納します。 構成ファイルはセットアップ時に作成され、インストールしたレポート サーバー インスタンスごとに存在します。 各ファイル内の値は、インストール中に設定されるか、ツールやアプリケーションを使用してサーバーの動作を構成したときに設定されます。 場合によっては、高度な設定を追加したり構成したりするために、ファイルを直接変更する必要があります。 構成設定は、XML 要素または XML 属性のいずれかとして指定されます。 XML ファイルおよび構成ファイルを理解している場合は、テキスト エディターまたはコード エディターを使用して、ユーザーが定義可能な設定を変更できます。  
  
 一部の構成設定は、ツールを使ってのみ設定できます。 暗号化された値を含んだ設定は、Reporting Services 構成ツール、セットアップ プログラム、または **rsconfig** コマンド ライン ユーティリティで変更する必要があります。 これらのツールを実行するには、ローカルの Administrators グループのメンバーである必要があります。  
  
> [!IMPORTANT]
>  構成ファイルを変更する場合は注意が必要です。 内部で使用するために予約されている設定を変更すると、インストールが無効になることがあります。 一般的に、特定の問題を解決しようとしている場合を除いて、構成設定を変更することはお勧めしません。 安全に変更できる設定の詳細については、「 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 」または「 [RSReportDesigner 構成ファイル](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)」を参照してください。 構成ファイルの詳細については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の製品ドキュメントを参照してください。  
  
 このトピックの内容  
  
-   [構成値の読み取りと使用](#bkmk_read_values)  
  
-   [既定値について](#bkmk_default_values)  
  
-   [構成設定の削除](#bkmk_delete_config_settings)  
  
-   [Reporting Services の構成ファイルを編集するには](#bkmk_edit_configuation_file)  
  
##  <a name="bkmk_read_values"></a> 構成値の読み取りと使用  
 レポート サーバーが構成ファイルを読み取るタイミングは、サービスが開始されたときと、構成ファイルが保存されたときです。 新しい値や変更された値は、現在のアプリケーション ドメインの有効期間が切れた後、新しいアプリケーション ドメインで有効になります。 現在のアプリケーション ドメインで処理中の要求は、できる限り最後まで完了するように配慮されます。 ただし、いくつかの設定については、アプリケーション ドメインのリサイクルが直ちに必要となります。 この場合、処理中の要求はすべて、新しいアプリケーション ドメインで再開されます。  
  
 無効な値が検出された場合、レポート サーバーによって Windows アプリケーション ログにエラーが記録され、エラーの内容に応じてレポート サーバーの起動が失敗するか、または既定値が使用されます。  
  
-   エラーの内容が不適切な形式の XML である場合は、レポート サーバーが起動されません。 レポート サーバーの実行中にエラーが発生した場合、レポート サーバーが再起動されるまで、またはアプリケーション ドメインのリサイクルが発生するまで、レポート サーバーは無効な構成ファイルを無視します。 エラーが検出されると、レポート サーバーは起動されなくなります。  
  
-   エラーの内容が無効な構成値である場合、内部の既定値が使用され、エラーがトレース ログ ファイルに記録されます。 サーバーの動作にきわめて重要な意味を持つ構成設定が無効であった場合で、かつ、内部の既定値が使用できないごく限られた状況では、サーバーから rsServerConfigurationError エラーが返されます。 設定が欠落している場合や、きわめて重要な設定が無効であった場合、クライアント アプリケーションには、それに関するエラーが HTML 形式のエラー ページとして返され、イベント ログに記録されます。  
  
 正常な変更も含め、構成ファイルに対するすべての変更は、レポート サーバーのトレース ログ ファイルに記録されます。 アプリケーション イベント ログには、エラーだけが記録されます。  
  
##  <a name="bkmk_default_values"></a> 既定値について  
 ほとんどの構成設定には、レポート サーバー内部で指定される既定値があります。 ユーザー定義の値が無効であったり、指定されていなかった場合は、既定値が使用されます。 構成設定が無効であるため既定値を使用した場合は、トレース ログ ファイルにエラーが書き込まれます。  
  
##  <a name="bkmk_delete_config_settings"></a> 構成設定の削除  
 既定値がある構成設定の場合は、構成ファイルから設定を削除しても影響はありません。 ほとんどの構成設定は、実際には内部的に定義および構成されます。 構成ファイルから項目を削除しても、内部コピーは引き続き使用でき、その項目に対して定義されている既定値が使用されます。  
  
##  <a name="bkmk_edit_configuation_file"></a> Reporting Services の構成ファイルを編集するには  
  
1.  編集する構成ファイルを探します。  
  
    -   **RSReportServer.config** は次のフォルダーにあります。  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
        ```  
        
        ||  
        |-|  
        |**[!INCLUDE[applies](../../includes/applies-md.md)]**  SQL Server Reporting Services での Power BI レポートの技術プレビュー (2017 年 1 月)|
        
        ```  
        C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
        ```
  
    -   **RSReportServerServices.exe.config** は次のフォルダーにあります。  
    
        > [!NOTE] 
        > これは、SQL Server Reporting Services の Power BI レポートの 2017 年 1 月 Technical Preview バージョンでは使用できません。
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin  
        ```  
  
    -   **RSReportDesigner.config** は次のフォルダーにあります。  
  
        ```  
        C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
        ```  
  
2.  変更をロールバックする必要がある場合は、ファイルのコピーを保存します。  
  
3.  元のファイルをメモ帳またはコード エディターで開きます。 Textpad は使用しないでください。ファイルの保存前にファイルの長さが設定されるため、無効な文字を示すエラーがトレース ログ ファイルに書き込まれます。  
  
4.  追加または使用する要素 (または値) を入力します。 要素では大文字と小文字が区別されます。 要素を追加する場合は、大文字と小文字を正しく区別して入力してください。 表示拡張機能、認証拡張機能、またはデータ処理拡張機能をカスタマイズしている場合は、対応する構成ファイルの編集方法を説明したトピックが用意されています。  
  
    -   [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)  
  
    -   [カスタム認証クッキーを送信するように Web ポータルを構成する](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
    -   [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
5.  ファイルを保存します。  
  
6.  トレース ログ ファイルを見て、エラーが発生していないことを確認します。 エラー状態が記録されていた場合は、設定またはその値が正しく指定されていません。 「 [RSReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 」を参照し、エラーの原因となっている設定について有効な値を確認してください。 トレース ログの表示方法の詳細については、「 [レポート サーバー サービスのトレース ログ](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [ReportingServicesService 構成ファイル](../../reporting-services/report-server/reportingservicesservice-configuration-file.md)   
 [RSReportDesigner 構成ファイル](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [データ処理拡張機能の配置](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [配信拡張機能の配置](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)   
 [表示拡張機能の配置](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)   
 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)  
  
  
