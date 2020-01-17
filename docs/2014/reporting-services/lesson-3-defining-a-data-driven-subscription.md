---
title: 'レッスン 3: データ ドリブン サブスクリプションの定義 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ee51a19d1dc169d2ae784d8a44403e021ff8b665
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108504"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>レッスン 3: データ ドリブン サブスクリプションの定義
  このレッスンでは、データ ドリブン サブスクリプションを使用し、サブスクリプション データ ソースへの接続、サブスクリプション データを取得するクエリの作成、および結果セットとレポート、配信オプションのマッピングを行います。  
  
> [!NOTE]  
>  開始する前に、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント サービスが実行されていることを確認します。 実行されていない場合は、サブスクリプションを保存できません。  
  
 このレッスンを行うには、レッスン 1 とレッスン 2 を完了していることと、レポート データ ソースに、保存された資格情報が使用されていることが必要です。  詳細については、「[レッスン 2: レポート データ ソースのプロパティの変更](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)」を参照してください  
  
 このトピックの内容  
  
-   [データ ドリブン サブスクリプション ウィザードを開始します。](#bkmk_startwizard)  
  
-   [手順 1 - 説明の定義](#bkmk_definesubscription)  
  
-   [手順 2 - サブスクライバー データ ソースへの接続を定義します。](#bkmk_defineconnectiontosubscriber)  
  
-   [手順 3 - データのサブスクライバーを取得するクエリの定義](#bkmk_definequery)  
  
-   [手順 4 - 配信オプションの設定](#bkmk_set_deliveryoptions)  
  
-   [手順 5 - レポート出力を変化させるパラメーター値を構成します。](#bkmk_configure_parameter)  
  
-   [手順 6 - サブスクリプションのスケジュール設定するには](#bkmk_schedule_subscription)  
  
##  <a name="bkmk_startwizard"></a> データ ドリブン サブスクリプション ウィザードを開始します。  
  
1.  レポート マネージャーで **[ホーム]** をクリックして **Sales Orders** レポートのあるフォルダーに移動します。  
  
2.  レポートのショートカット メニューで、 **[管理]** をクリックし、 **[サブスクリプション]** タブをクリックします。  
  
3.  クリックして**新しいデータ ドリブン サブスクリプション**します。 このボタンが表示されない場合は、コンテンツ マネージャーの権限がありません。  
  
##  <a name="bkmk_definesubscription"></a> 手順 1 - 説明の定義  
  
1.  説明に「 **Sales Order delivery** 」と入力します。  
  
2.  **[受信者への通知方法を指定します]** で **[Windows ファイル共有]** を選択します。  
  
3.  **[このサブスクリプションのみを対象とします]** を選択し、 **[次へ]** をクリックします。  
  
##  <a name="bkmk_defineconnectiontosubscriber"></a> 手順 2 - サブスクライバー データ ソースへの接続を定義します。  
  
1.  データ ソースの種類として **[Microsoft SQL Server]** を選択します。  
  
2.  [接続文字列] に、次のように入力します。  
  
    ```  
    data source=localhost; initial catalog=Subscribers  
    ```  
  
    > [!NOTE]  
    >  サブスクライバーは、レッスン 1 で作成したデータベースです。  
  
3.  **[レポート サーバーに保存され、セキュリティで保護された資格情報]** をクリックします。  
  
4.  **[ユーザー名]** と **[パスワード]** に、ドメイン ユーザー名とパスワードを入力します。 **[ユーザー名]** には、ドメインとユーザー アカウントの両方を指定します。  
  
    > [!NOTE]  
    >  サブスクライバー データ ソースへの接続に使用する資格情報は、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]に返されません。 後でサブスクリプションを変更する場合は、データ ソースへの接続に使用するパスワードをこのページで再入力する必要があります。  
  
5.  **[データ ソースへの接続時に Windows 資格情報として使用する]** をクリックし、 **[次へ]** をクリックします。  
  
##  <a name="bkmk_definequery"></a> 手順 3 - データのサブスクライバーを取得するクエリの定義  
  
1.  クエリ ボックスに次のクエリを入力します。  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  30 秒のタイムアウトを指定します。  
  
3.  **[検証]** をクリックし、 **[次へ]** をクリックします。  
  
##  <a name="bkmk_set_deliveryoptions"></a> 手順 4 - 配信オプションの設定  
  
1.  **[ファイル名]** で、 **[データベースから値を取得]** を選択します。 **Order**フィールドをクリックします。  
  
2.  **[パス]** で、 **[静的な値を指定]** を選択します。 [値の設定] に、書き込み権限のあるパブリック ファイル共有の名前を入力します (例: `\\mycomputer\public\myreports`)。  
  
3.  **[表示形式]** で、 **[データベースから値を取得]** を選択します。 **[書式]** を選択します。  
  
4.  **[書き込みモード]** で、 **[静的な値を指定]** をクリックし、 **[自動増分]** を選択します。  
  
5.  **[ファイル拡張子]** で、 **[静的な値を指定]** を選択し、 **[True]** を選択します。  
  
6.  **[ユーザー名]** で、 **[静的な値を指定]** を選択します。 ドメイン ユーザー アカウントを入力します。 `<domain>\<account>`の形式で入力してください。 ユーザー アカウントには、前の手順で構成したパスに対する権限が必要です。  
  
7.  **[パスワード]** で、 **[静的な値を指定]** を選択します。 パスワードを入力します。 パスワードは正確に入力してください。 このウィザードでは、パスワードは検証されません。  
  
8.  **[次へ].**  
  
##  <a name="bkmk_configure_parameter"></a> 手順 5 - レポート出力を変化させるパラメーター値を構成します。  
  
1.  **[OrderNumber]** には、 **[データベースから値を取得]** を選択します。 [値] で、 **[Order]** をクリックします。 **[次へ].**  
  
##  <a name="bkmk_schedule_subscription"></a> 手順 6 - サブスクリプションのスケジュール設定するには  
  
1.  **[このサブスクリプション用に作成されたスケジュールで実行]** をクリックし、 **[次へ]** をクリックします。  
  
2.  **[スケジュールの詳細]** で、 **[一度だけ]** をクリックします。  
  
3.  開始時刻として、現在の時刻から数分後を指定します。  
  
4.  **[完了]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 サブスクリプションを実行すると、 *Subscribers* データ ソースの注文ごとに 1 つずつ、4 つのレポート ファイルが、指定したファイル共有に配信されます。 各配信では、データ (注文固有のデータ)、表示形式、ファイル形式がそれぞれ異なっています。 各レポートを共有フォルダーから開き、定義したサブスクリプション オプションに基づいて各バージョンがカスタマイズされているかどうかを確認できます。  
  
 ![サブスクリプションによって作成されるファイルの一覧](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-filelist.gif "サブスクリプションによって作成されるファイルの一覧")  
  
 レポート マネージャーのサブスクリプション ページには、サブスクリプションの **[最終実行]** 日付と **[状態]** が表示されます。  
  
> [!NOTE]  
>  サブスクリプションを実行した後、ページを更新して更新後の情報を表示します。  
  
 ![レポート マネージャーでのサブスクリプションの結果](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.gif "レポート マネージャーでのサブスクリプションの結果")  
  
 これで、「データ ドリブン サブスクリプションの定義」のチュートリアルは終了します。 詳細については、その他は[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]チュートリアルを参照してください[Reporting Services のチュートリアル&#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)します。  
  
## <a name="see-also"></a>参照  
 [データ ドリブン サブスクリプションの作成 &#40;SSRS チュートリアル&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [サブスクリプションと配信 &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [データ ドリブン サブスクリプション](subscriptions/data-driven-subscriptions.md)   
 [作成、変更、およびデータ ドリブン サブスクリプションの削除](subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [サブスクライバー データに対して外部データ ソースを使用する &#40;データ ドリブン サブスクリプション&#41;](subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
