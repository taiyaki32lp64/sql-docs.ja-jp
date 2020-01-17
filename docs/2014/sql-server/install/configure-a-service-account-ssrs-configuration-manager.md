---
title: サービスアカウントの構成 (SSRS Configuration Manager) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Server Web service, accounts
- service accounts [Reporting Services]
- Report Server Windows service, accounts
- Web service [Reporting Services], report server
ms.assetid: 25000ad5-3f80-4210-8331-d4754dc217e0
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 04dff943d1227f84ff514e593f65c2ce4d7a918f
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952585"
---
# <a name="configure-a-service-account-ssrs-configuration-manager"></a>サービス アカウントの構成 (SSRS 構成マネージャー)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] がインストールされた環境では、レポート サーバー Web サービス、レポート マネージャー、およびバックグラウンド処理アプリケーションが 1 つのサービス内で実行されます。 サービスの実行に使用するアカウントは、セットアップ時に [サービス ID] ページでアカウントを指定するときに定義されますが、使用するアカウントの変更やパスワードの更新を行う場合は、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用できます。  
  
 SharePoint 統合モードを使用するように構成されているレポートサーバーがあり、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用してサービスアカウントを変更する場合は、SharePoint サーバーの全体管理を開き、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の **[データベースアクセスの許可]** ページを使用して、レポートサーバーとインスタンスの設定を再適用する必要もあります。 この手順により、新しいサービスアカウントに SharePoint データベースへのアクセス権が付与されます。これは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] または [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]と統合するために必要です。  
  
 サービス アカウントを更新する際には、そのサービス ID に依存する他の設定も同時に更新できるように、必ず [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用してください。  
  
> [!NOTE]  
>  ドメイン コントローラーになっているコンピューターでは、ビルトイン Windows サービス アカウント (Local Service または Network Service) をレポート サーバーのサービス アカウントとして使用することはできません。  
  
 手順  
  
### <a name="to-configure-the-report-server-service-account"></a>レポート サーバー サービス アカウントを構成するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを起動して、レポート サーバーに接続します。  
  
2.  [サービス アカウント] ページで、使用するアカウントの種類を示すオプションを選択します。 指定するアカウントの種類に関する推奨事項については、「[レポート&#40;サーバーサービス&#41;アカウントの SSRS Configuration Manager の構成](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)」を参照してください。  
  
3.  Windows ユーザー アカウントを選択した場合は、新しいアカウントとパスワードを指定します。 アカウントは 20 文字以下にする必要があります。  
  
     レポート サーバーが Kerberos 認証をサポートするネットワークに配置されている場合、指定したドメイン ユーザー アカウントでレポート サーバーのサービス プリンシパル名 (SPN) を登録する必要があります。 詳細については、「[レポート サーバーのサービス プリンシパル名 &#40;SPN&#41; の登録](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)」を参照してください。  
  
4.  **[適用]** をクリックします。  
  
5.  対称キーをバックアップするかどうかを確認するメッセージが表示されたら、対称キーのバックアップ用のファイル名と場所を入力し、ファイルをロックおよびロック解除するためのパスワードを入力して **[OK]** をクリックします。  
  
6.  レポート サーバーがサービス アカウントを使用してレポート サーバー データベースに接続する場合は、新しいアカウントまたはパスワードを使用するように接続情報が更新されます。 接続情報を更新するには、データベースに接続する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **[データベース接続]** ダイアログ ボックスが表示されたら、データベースに接続する権限を持つ資格情報を入力し、 **[OK]** などのビルトイン アカウントで実行できます。  
  
7.  対称キーを復元するかどうかを確認するメッセージが表示されたら、手順 5. で指定したパスワードを入力し、 **[OK]** をクリックします。  
  
8.  [結果] ペインに表示される状態メッセージで、すべてのタスクが正常に完了したことを確認します。  
  
## <a name="troubleshooting-service-identity-update-errors"></a>サービス ID の更新エラーのトラブルシューティング  
 サービス ID を変更すると、一連のイベントが開始されます。サービスが再起動され、パスワードで保護された暗号化キーが更新され、URL 予約が更新されます。また、サービス アカウントを使用してレポート サーバー データベースに接続している場合は、レポート サーバー データベースの接続情報が更新されます。 これらのイベントの状態を監視するには、ページの下部にある [結果] パネルで通知を確認します。 この処理中にエラーが発生した場合は、解決方法として次の方法を試してください。  
  
-   対称キーを復元できない場合は、[暗号化キー] ページの **[復元]** を使用して、手動で復元を試行できます。 それでも復元できない場合は、暗号化されたコンテンツを削除することを検討してください。 データ ソース接続情報およびサブスクリプションは再作成する必要がありますが、残りのコンテンツはそのまま使用できます。 詳細については、「 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。  
  
-   サービスが開始されない場合は、[管理ツール] の Services コンソール アプリケーションを使用して、手動で再起動します。  
  
-   URL 予約エラーは、サービス アカウントを更新するときに発生する可能性があります。 各 URL 予約には、URL に対する要求を受け入れる権限をサービス アカウントに許可する任意のアクセス制御リスト (DACL) を含むセキュリティ記述子が含まれています。 アカウントの更新時に、URL を再作成して新しいアカウント情報で DACL を更新する必要があります。 URL 予約を再作成できない場合、アカウントが有効であるとわかっているときは、コンピューターを再起動してください。 エラーが引き続き発生する場合は、別のアカウントを使用してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー データベース接続の構成 &#40;SSRS 構成マネージャー&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [サービスアカウント&#40;SSRS ネイティブモード&#41; ](../../../2014/sql-server/install/service-account-ssrs-native-mode.md)   
 [暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
