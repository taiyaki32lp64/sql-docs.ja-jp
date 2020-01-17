---
title: SCOM で監視する
description: Analytics Platform System の System Center Operations Manager (SCOM) 管理パックを構成するには、次の手順に従います。 SCOM から Analytics Platform System を監視するには、管理パックが必要です。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 67029d235a1bc65b5ee0ab6f01f51dea42ebcc8b
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401300"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Analytics Platform System を監視するように System Center Operations Manager (SCOM) を構成する
Analytics Platform System の System Center Operations Manager (SCOM) 管理パックを構成するには、次の手順に従います。 SCOM から Analytics Platform System を監視するには、管理パックが必要です。  
  
## <a name="BeforeBegin"></a>開始する前に  
**前提条件**  
  
System Center Operations Manager 2007 R2 がインストールされ、実行されている必要があります。  
  
管理パックをインストールして構成する必要があります。 「 [Scom 管理パック &#40;Analytics Platform system&#41;をインストールする](install-the-scom-management-packs.md)」および「 [PDW &#40;analytics platform SYSTEM&#41;の scom 管理パックをインポート](import-the-scom-management-pack-for-pdw.md)する」を参照してください。  
  
## <a name="ConfigureRunAsProfile"></a>System Center での実行プロファイルの構成  
System Center を構成するには、次の手順を実行する必要があります。  
  
-   **APS 監視**ドメインユーザーの実行アカウントを作成し、 **Microsoft aps ウォッチャーアカウント**にマップします。  
  
-   **Monitoring_user** APS ユーザーの実行アカウントを作成し、 **Microsoft aps アクションアカウント**にマップします。  
  
ここでは、タスクを実行する方法について詳しく説明します。  
  
1.  **Aps**監視ドメインユーザーの**Windows**アカウントの種類を使用して、 **aps 監視**の実行アカウントを作成します。  
  
    1.  [**管理**] ウィンドウに移動し、[**実行構成** -> **アカウント**] を右クリックして、[**実行アカウントの作成**] を選択します。  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  [**実行アカウントの作成ウィザード**] ダイアログボックスが開きます。 
  **[説明]** ページで **[次へ]** をクリックします。  
  
    3.  [**全般プロパティ**] ページで、[**実行アカウントの種類**] で [ **Windows** ] を選択し、**表示名**として "APS Watcher" を指定します。  
  
        ![Createrunasaccountwizardproperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "Createrunasaccountwizardproperties")  
  
    4.  [**資格情報**] ページで、 ![Createrunasaccountwizardcredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")を入力します。  
  
    5.  [**配布セキュリティ**] ページで、[**低セキュリティ**] を選択し、[**作成**] ボタンをクリックして完了します。  
  
        ![Createrunasaccountwizardのセキュリティ](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "Createrunasaccountwizardのセキュリティ")  
  
        1.  **より安全な**オプションを使用する場合は、資格情報が配布されるコンピューターを手動で指定する必要があります。 これを行うには、実行アカウントを作成した後、それを右クリックし、[**プロパティ**] を選択します。  
  
        2.  [**配布**] タブに移動し、目的のコンピュータを**追加**します。  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  **MICROSOFT Aps 監視アカウント**プロファイルを、 **aps ウォッチャー**の実行アカウントを使用するように設定します。  
  
    1.  [**管理** -> ] [実行] [**構成** -> **プロファイル**] に移動します。  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  一覧から [ **MICROSOFT APS Watcher アカウント**] を右クリックし、[**プロパティ**] を選択します。  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  [**実行プロファイルウィザード**] ダイアログボックスが開きます。 [**次へ**] をクリックして、[**はじめ**に] ページをスキップします。  
  
    4.  [**全般プロパティ**] ページで、[**次へ**] をクリックします。  
  
    5.  [**実行アカウント**] ページで、[**追加**] ボタンをクリックし、以前に作成した**APS ウォッチャー**の実行アカウントを選択します。  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  [**保存**] をクリックしてプロファイルの割り当てを完了します。  
  
3.  APS アプライアンスの検出が完了するまで待ちます。  
  
    1.  [**監視**] ウィンドウに移動し、 **SQL Server アプライアンス** -> **Microsoft Analytics Platform System** -> **アプライアンス**の状態ビューを開きます。  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  アプライアンスが一覧に表示されるまで待ちます。 アプライアンスの名前は、レジストリに指定されているものと同じである必要があります。 検出が完了すると、すべてのアプライアンスが一覧表示されますが、監視対象にはなりません。 監視を有効にするには、次の手順に従います。  
  
    > [!NOTE]  
    > 次の手順は、最初のアプライアンスの検出が終了するのを待機している間に、並行して完了することができます。  
  
4.  別の新しい実行アカウントを作成し、正常性データの取得のために APS を照会します。  
  
    1.  手順 1. で説明されているように、新しい実行アカウントの作成を開始します。  
  
    2.  [**全般プロパティ**] ページで、[**基本認証**アカウントの種類] を選択します。  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  [**資格情報**] ページで、APS 正常性状態 dmv にアクセスするための有効な資格情報を指定します。  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  APS インスタンスに新しく作成された実行アカウントを使用するように**MICROSOFT Aps アクションアカウント**プロファイルを構成します。  
  
    1.  手順 2. の説明に従って、 **MICROSOFT APS アクションアカウント**のプロパティに移動します。  
  
    2.  [**実行アカウント**] ページで、[**追加...** ] をクリックし、 
    3.  新しく作成した実行アカウントを選択します。  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>次のステップ  
管理パックの構成が完了したので、アプライアンスの監視を開始する準備ができました。 詳細については、「 [System Center Operations Manager &#40;Analytics Platform System&#41;を使用したアプライアンスの監視](monitor-the-appliance-by-using-system-center-operations-manager.md)」を参照してください。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
