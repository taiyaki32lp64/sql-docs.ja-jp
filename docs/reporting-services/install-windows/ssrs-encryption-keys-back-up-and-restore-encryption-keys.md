---
title: Reporting Services の暗号化キーのバックアップと復元 | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- backing up encryption keys [Reporting Services]
- restoring encryption keys [Reporting Services]
- encryption keys [Reporting Services]
- symmetric keys [Reporting Services]
ms.assetid: 6773d5df-03ef-4781-beb7-9f6825bac979
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3a1066e06ca5a526cbfa4cb6f7d54014e4ef520d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65502850"
---
# <a name="ssrs-encryption-keys---back-up-and-restore-encryption-keys"></a>SSRS の暗号化キー - 暗号化キーのバックアップと復元
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  レポート サーバー構成で重要なのは、機密情報の暗号化に使用される対称キーのバックアップ コピーの作成です。 キーのバックアップ コピーは多くのルーチン処理で必要とされ、キーのバックアップ コピーにより新しいインストールで既存のレポート サーバー データベースを再利用できます。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
 次のいずれかが行われた場合、暗号化キーのバックアップ コピーを復元する必要があります。  
  
-   レポート サーバー Windows サービスのアカウント名の変更またはパスワードの再設定。 Reporting Services 構成マネージャーを使用する際に、サービス アカウント名の変更操作の一部としてキーをバックアップします。  
  
    > [!NOTE]
    > パスワードの再設定はパスワードの変更とは異なります。 パスワードを再設定するには、ドメイン コントローラーでアカウント情報を上書きする権限が必要です。 パスワードの再設定は、ユーザーが特定のパスワードを忘れた場合、または知らない場合に、システム管理者が行います。 パスワードの再設定にのみ、対称キーの復元が必要となります。 アカウント パスワードの定期的な変更には、対称キーの再設定は必要ありません。  
  
-   レポート サーバーをホストするコンピューターまたはインスタンスの名前変更 (レポート サーバー インスタンスは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名に基づいています)。  
  
-   レポート サーバー インストールの移行または別のレポート サーバー データベースを使用するようにレポート サーバーを構成。  
  
-   ハードウェア障害による、レポート サーバー インストールの復旧。  
  
 対称キーに必要なバックアップのコピーは 1 つだけです。 レポート サーバー データベースと対称キーは、一対一で対応します。 必要なバックアップのコピーは 1 つだけですが、スケールアウト配置モデルで複数のレポート サーバーを起動している場合には、複数回キーを復元する必要が生じる場合があります。 各レポート サーバー インスタンスは、レポート サーバー データベースでデータをロックおよびロック解除するために対称キーのコピーが必要になります。

 対称キーのバックアップは、指定するファイルにキーを書き込み、指定したパスワードを使用してそのキーにスクランブルをかける処理です。 対称キーが暗号化されていない状態で格納されることはないので、ディスクに格納する際は、キーを暗号化するためのパスワードを指定する必要があります。 ファイルの作成後、セキュリティで保護された場所にファイルを保存します。ファイルのロックを解除するために使用する **パスワードを覚えておく** 必要があります。 対称キーをバックアップするために、次のツールを使用できます。  
  
 **ネイティブ モード:** Reporting Services 構成マネージャーか **rskeymgmt** ユーティリティのどちらか。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
 **SharePoint モード:** SharePoint サーバーの全体管理ページまたは PowerShell。  
  
##  <a name="bkmk_backup_sharepoint"></a> SharePoint モードのレポート サーバーのバックアップ  
 SharePoint モードのレポート サーバーの場合は、PowerShell コマンドを使用するか、または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの管理ページを使用します。 詳細については、「[Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)」の「キー管理」のセクションを参照してください。  

::: moniker-end
  
##  <a name="bkmk_backup_configuration_manager"></a> 暗号化キーのバックアップ - Reporting Services 構成マネージャー (ネイティブ モード)  
  
1.  レポート サーバーの構成マネージャーを起動して、構成するレポート サーバー インスタンスに接続します。  
  
2.  **[暗号化キー]** をクリックし、次に **[バックアップ]** をクリックします。  
  
3.  複雑なパスワードを入力します。  
  
4.  格納されたキーを含むファイルを指定します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、ファイルに .snk ファイル拡張子が付けられます。 このファイルを、レポート サーバーとは別のディスクに保存することを検討してください。  
  
5.  **[OK]** を選択します。  
  
###  <a name="bkmk_backup_rskeymgmt"></a> 暗号化キーのバックアップ - rskeymgmt (ネイティブ モード)  
  
1.  レポート サーバーをホストするコンピューターのローカルで **rskeymgmt.exe** を実行します。 抽出用の **-e** 引数を使用してキーをコピーし、ファイル名を入力して、パスワードを指定する必要があります。 指定する必要がある引数の例を次に示します。  
  
    ```  
    rskeymgmt -e -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="restore-encryption-keys"></a>暗号化キーの復元  
 対称キーを復元すると、レポート サーバー データベースに格納されている既存の対称キーを上書きします。 暗号化キーを復元すると、使用できないキーが以前ディスクに格納したコピーと置き換わります。 暗号化キーを復元することにより、次の処理が行われます。  
  
-   パスワードで保護されたバックアップ ファイルで対称キーが開きます。  
  
-   レポート サーバー Windows サービスの公開キーを使用して、対称キーが暗号化されます。  
  
-   暗号化された対称キーがレポート サーバー データベースに格納されます。  
  
-   以前格納した対称キー データ (以前の配置から既にレポート サーバー データベースにあったキー情報など) は削除されます。  
  
 暗号化キーを復元するには、暗号化キーのコピーがファイルにある必要があります。 また、格納したコピーのロックを解除するパスワードを知っている必要もあります。 キーおよびパスワードがある場合、Reporting Services 構成ツールまたは **rskeymgmt** ユーティリティを実行して、キーを復元できます。 対称キーは、レポート サーバー データベースに現在格納されている暗号化されたデータをロックおよびロック解除するキーと同じものである必要があります。 有効ではないコピーを復元すると、レポート サーバーは、レポート サーバー データベースに現在格納されている暗号化されたデータにアクセスできません。 暗号化されたデータにアクセスできず、有効なキーを復元できない場合、すべての暗号化された値を削除する必要が生じることがあります。 なんらかの理由で暗号化キーを復元できない場合 (バックアップ コピーがない場合など)、既存のキーおよび暗号化されたコンテンツを削除する必要があります。 詳細については、「[暗号化キーの削除と再作成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)」を参照してください。 対称キーの作成の詳細については、「[レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)」を参照してください。  
  
###  <a name="bkmk_restore_configuration_manager"></a> 暗号化キーの復元 - Reporting Services 構成マネージャー (ネイティブ モード)  
  
1.  Reporting Services 構成マネージャーを起動して、構成するレポート サーバー インスタンスに接続します。  
  
2.  [暗号化キー] ページで、 **[復元]** をクリックします。  
  
3.  バックアップ コピーを含む .snk ファイルを選択します。  
  
4.  ファイルのロックを解除するパスワードを入力します。  
  
5.  **[OK]** を選択します。 
  
###  <a name="bkmk_restore_rskeymgmt"></a> 暗号化キーの復元 - rskeymgmt (ネイティブ モード)  
  
1.  レポート サーバーをホストするコンピューターのローカルで **rskeymgmt.exe** を実行します。 キーを復元するには、 **-a** 引数を使用します。 完全修飾ファイル名を入力し、パスワードを指定する必要があります。 指定する必要がある引数の例を次に示します。  
  
    ```  
    rskeymgmt -a -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="see-also"></a>参照  
 [暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
