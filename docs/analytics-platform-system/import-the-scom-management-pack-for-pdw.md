---
title: SCOM 管理パックのインポート
description: Analytics Platform System (APS) 用の System Center Operations Manager (SCOM) 管理パックをインポートするには、次の手順に従います。 SCOM から並列データウェアハウスを監視するには、管理パックが必要です。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bcb0e667424767fd53a5fc7e027e84d512022203
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401081"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>SCOM 管理パックのインポート-Analytics Platform System
Analytics Platform System (APS) 用の System Center Operations Manager (SCOM) 管理パックをインポートするには、次の手順に従います。 SCOM から並列データウェアハウスを監視するには、管理パックが必要です。 
  
## <a name="BeforeBegin"></a>開始する前に  
**前提条件**  
  
System Center Operations Manager 2007 R2 がインストールされ、実行されている必要があります。  
  
管理パックをインストールする必要があります。 「 [Analytics Platform System&#41;&#40;SCOM 管理パックをインストールする](install-the-scom-management-packs.md)」を参照してください。  
  
## <a name="Step1"></a>手順 1: SQL Server アプライアンスベースの管理パックをインポートする  
  
1.  Operations Manager 2007 管理グループの Operations Manager Administrators ロールのメンバーであるアカウントで、コンピューターにログオンします。  
  
2.  オペレーション コンソールで、[管理]**** をクリックします。  
  
3.  [**管理パック**] ノードを右クリックし、[**管理パックのインポート**] をクリックします。  
  
    ![[管理パックのインポート] をクリック](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  管理パックの一覧で、インポートする管理パックを選択し、[**選択**] をクリックして、[**追加**] をクリックします。  
  
    ![管理パックの一覧](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  **アプライアンス**を検索し、SQL Server アプライアンスベースにドリルダウンしてから、[2 つの選択肢を**追加**する] をクリックします。  
  
    ![SQL Server アプライアンス ベース](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  2つの管理パックが下部の選択ウィンドウに表示されたら、[ **OK]** をクリックします。  
  
    ![両方の管理パックを選択](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  
  **[インストール]** をクリックします。  
  
    ![[インストール] をクリックします。](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  完了したら、[**閉じる**] をクリックします。  
  
    ![完了後、[閉じる] をクリック](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Microsoft SQL Server 2008 R2 並列データウェアハウスアプライアンス用監視パックをインポートする  
  
1.  [**管理パック**] ノードを右クリックし、[**管理パックのインポート**] をクリックします。  
  
2.  [**ディスクから追加**...] を選択します。  
  
    ![[管理パックのインポート] を右クリック](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  SQL Server PDW 管理パックを展開した場所に移動し、[インポートする管理パックを選択してください] セクションにある3つの管理パックを選択します。 これを行うには、最初の1つを選択し、[Shift] をクリックして、最後のキーを選択します。 すべて選択したら、[**開く**] をクリックします。  
  
    ![管理パックの選択](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  
  **[インストール]** をクリックします。  
  
    ![[インストール] をクリックします。](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  [**閉じる**] をクリックします。  
  
    ![[閉じる] をクリックしてください](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>次のステップ  
管理パックをインポートしたので、次の手順「 [Analytics Platform system &#40;Analytics Platform system&#41;を監視するように SCOM を構成](configure-scom-to-monitor-analytics-platform-system.md)する」に進みます。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
