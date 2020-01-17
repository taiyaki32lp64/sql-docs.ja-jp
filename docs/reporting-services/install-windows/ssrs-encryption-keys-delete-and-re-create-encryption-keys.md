---
title: 暗号化キーの削除と再作成 (SSRS 構成マネージャー) | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- re-creating encryption keys
- encryption keys [Reporting Services]
- deleting encryption keys
- symmetric keys [Reporting Services]
- removing encryption keys
- resetting encryption keys
ms.assetid: 201afe5f-acc9-4a37-b5ec-121dc7df2a61
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5bf83ea3eb7ed7f4ef28872b964449d2924aab48
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593533"
---
# <a name="ssrs-encryption-keys---delete-and-re-create-encryption-keys"></a>SSRS の暗号化キー - 暗号化キーの削除と再作成
  暗号化キーの削除および再作成は、日常の暗号化キー メンテナンスには該当しない作業です。 レポート サーバーに対する特定の脅威への対処、またはレポート サーバー データベースにアクセスできなくなったときの最後の手段としてこの作業を行ってください。  
  
-   既存の対称キーに障害が発生したと考えられる場合は対称キーを再作成します。 セキュリティを重視する場合は、定期的にキーを再作成することもできます。  
  
-   対称キーを復元できない場合は、既存の暗号化キーと使用できない暗号化コンテンツを削除します。  
  
## <a name="re-creating-encryption-keys"></a>暗号化キーの再作成  
 対称キーが不正なユーザーに知られた場合、またはレポート サーバーが攻撃を受けたために予防策として対称キーの再設定が必要な場合、対称キーを再作成することができます。 対称キーを再作成すると、暗号化されたすべての値が新しい値で再暗号化されます。 スケールアウト配置で複数のレポート サーバーを実行している場合、対称キーのすべてのコピーが新しい値に更新されます。 レポート サーバーは利用可能な公開キーを使用して、配置を構成する各サーバーの対称キーを更新します。  
  
 対称キーを再作成できるのは、レポート サーバーが動作中の場合のみです。 暗号化キーの再作成およびコンテンツの再暗号化を実行すると、サーバーの処理が中断されます。 再暗号化の実行中はサーバーをオフラインにする必要があります。 再暗号化中にレポート サーバーに対して要求を送信することはできません。  
  
 対称キーおよび暗号化データを再設定するには、Reporting Services 構成ツールまたは **rskeymgmt** ユーティリティを使用できます。 対称キーの作成方法の詳細については、「[レポート サーバーの初期化 (SSRS 構成マネージャー)](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)」を参照してください。  
  
### <a name="how-to-re-create-encryption-keys-reporting-services-configuration-tool"></a>暗号化キーの再作成方法 (Reporting Services 構成ツール)  
  
1.  rsreportserver.confi ファイルで **IsWebServiceEnabled** プロパティを変更することにより、レポート サーバー Web サービスおよび HTTP アクセスを無効にします。 この手順を実行すると、レポート サーバーへの認証要求の送信が一時的に停止されますが、レポート サーバーが完全にシャットダウンされることはありません。 キーを再作成できるように最小限のサービスが必要です。  
  
     レポート サーバーのスケールアウト配置に対する暗号化キーを再作成する場合、配置内のすべてのインスタンスでこのプロパティを無効にします。  
  
    1.  Windows エクスプローラーを開き、 *drive*:\Program Files\Microsoft SQL Server\\*report_server_instance*\Reporting Services に移動します。 *drive* は使用しているコンピューターのドライブ文字に置き換え、 *report_server_instance* は Web サービスおよび HTTP アクセスを無効にするレポート サーバー インスタンスに対応するフォルダー名に置き換えます。 たとえば、C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services のようになります。  
  
    2.  rsreportserver.config ファイルを開きます。  
  
    3.  **IsWebServiceEnabled** プロパティには、 **False**を指定してから変更内容を保存します。  
  
2.  Reporting Services 構成ツールを起動して、構成するレポート サーバー インスタンスに接続します。  
  
3.  [暗号化キー] ページで、 **[変更]** をクリックします。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  レポート サーバー Windows サービスを再開します。 レポート サーバーのスケールアウト配置に対する暗号化キーを再作成する場合、すべてのインスタンスでサービスを再起動します。  
  
5.  rsreportserver.confi ファイルで **IsWebServiceEnabled** プロパティを変更することにより、Web サービスおよび HTTP アクセスを再び有効にします。 スケールアウト配置の場合は、すべてのインスタンスについてこの作業を行います。  
  
### <a name="how-to-re-create-encryption-keys-rskeymgmt"></a>暗号化キーの再作成方法 (rskeymgmt)  
  
1.  レポート サーバー Web サービスおよび HTTP アクセスを無効にします。 上記の手順に従って Web サービスの操作を停止します。  
  
2.  レポート サーバーをホストするコンピューターのローカルで **rskeymgmt.exe** を実行します。 **-s** 引数を使用して対称キーを再設定します。 他の引数は必要ありません。  
  
    ```  
    rskeymgmt -s  
    ```  
  
3.  Reporting Services の Windows サービスを再起動します。  
  
## <a name="deleting-unusable-encrypted-content"></a>使用できない暗号化コンテンツの削除  
 何らかの理由で暗号化キーを復元できない場合、レポート サーバーはこのキーによって暗号化されたデータの暗号化を解除して使用することができません。 レポート サーバーを動作中の状態に戻すには、レポート サーバー データベースに格納されている暗号化された値を削除して、必要な値を手動で再指定する必要があります。  
  
 暗号化キーを削除すると、対称キーの情報がすべてレポート サーバー データベースから削除され、また暗号化されたコンテンツもすべて削除されます。 暗号化されていないデータはそのまま残ります。削除されるのは暗号化されたコンテンツだけです。 暗号化キーを削除した場合、レポート サーバーは新しい対称キーを追加することでレポート サーバー自体を自動的に再初期化します。 暗号化されたコンテンツを削除すると、以下の処理が実行されます。  
  
-   共有データ ソースの接続文字列が削除されます。 レポートを実行しているユーザーに対して "ConnectionString プロパティが初期化されていません。" というエラーが表示されます。  
  
-   保存されている資格情報が削除されます。 レポートおよび共有データ ソースは、要求された資格情報を使用するように再構成されます。  
  
-   モデルを基にしたレポートは実行されません (また、保存されている資格情報を使用するか、または資格情報を使用しないように構成された共有データ ソースを必要とするレポートも実行されません)。  
  
-   サブスクリプションが非アクティブになります。  
  
 暗号化されたコンテンツをいったん削除したら、そのコンテンツを復旧することはできません。 接続文字列および保存された資格情報を再指定して、サブスクリプションをアクティブにする必要があります。  
  
 値を削除するには、Reporting Services 構成ツールまたは **rskeymgmt** ユーティリティを使用できます。  
  
### <a name="how-to-delete-encryption-keys-reporting-services-configuration-tool"></a>暗号化キーの削除方法 (Reporting Services 構成ツール)  
  
1.  Reporting Services 構成ツールを起動して、構成するレポート サーバー インスタンスに接続します。  
  
2.  **[暗号化キー]** をクリックし、 **[削除]** をクリックします。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  レポート サーバー Windows サービスを再開します。 スケールアウト配置の場合は、すべてのレポート サーバー インスタンスについてこの作業を行います。  
  
### <a name="how-to-delete-encryption-keys-rskeymmgt"></a>暗号化キーの削除方法 (rskeymmgt)  
  
1.  レポート サーバーをホストするコンピューターのローカルで **rskeymgmt.exe** を実行します。 削除用の **-d** 引数を使用する必要があります。 指定する必要がある引数の例を次に示します。  
  
    ```  
    rskeymgmt -d  
    ```  
  
2.  レポート サーバー Windows サービスを再開します。 スケールアウト配置の場合は、すべてのレポート サーバー インスタンスについてこの作業を行います。  
  
### <a name="how-to-re-specify-encrypted-values"></a>暗号化された値を再指定する方法  
  
1.  各共有データ ソースに対して、接続文字列を再入力する必要があります。  
  
2.  保存された資格情報を使用するレポートおよび共有データ ソースごとに、ユーザー名とパスワードを再入力して、これらの情報を保存する必要があります。 詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)」をご覧ください。  
  
3.  各データ ドリブン サブスクリプションを開いて、資格情報をサブスクリプション データベースに再入力します。  
  
4.  暗号化されたデータ (ファイル共有の配信拡張機能や暗号化を使用するサードパーティ製の配信拡張機能など) を使用する各サブスクリプションを開いて、資格情報を再入力します。 レポート サーバーの電子メール配信を使用するサブスクリプションでは、暗号化されたデータが使用されないため、キーの変更による影響を受けません。  
  
## <a name="see-also"></a>参照  
 [暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
