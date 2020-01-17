---
title: SCOM 管理パックをインストールする
description: SQL Server PDW 用の System Center Operations Manager (SCOM) 管理パックをダウンロードしてインストールするには、次の手順に従います。 SCOM から SQL Server PDW を監視するには、管理パックが必要です。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3652b767f4628b61f5dd363999838418ff933aa
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401072"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>Analytics Platform System 用 SQL Server Operations Manager (SCOM) 管理パックをインストールする
SQL Server PDW 用の System Center Operations Manager (SCOM) 管理パックをダウンロードしてインストールするには、次の手順に従います。 SCOM から SQL Server PDW を監視するには、管理パックが必要です。  
  
## <a name="BeforeBegin"></a>開始する前に  
**前提条件**  
  
System Center Operations Manager をインストールして実行する必要があります。 SQL Server PDW 2012 では System Center Operations Manager 2007 R2、System Center Operations Manager 2012、または System Center Operations Manager 2012 Service Pack 1 が必要です。  
  
## <a name="Step1"></a>手順 1: 管理パックをダウンロードする  
APS PDW ワークロードの場合は、 [Microsoft Analytics Platform System 用の System Center 管理パック](https://go.microsoft.com/fwlink/?LinkId=396857)をダウンロードします。  
  
アプライアンス管理については、 [SQL Server アプライアンスベース管理パック](https://docs.microsoft.com/previous-versions/system-center/packs/gg602398(v=technet.10))をダウンロードしてください。  
  
APS を使用していない PDW の旧バージョンについては、[Microsoft SQL Server 2012 並列データウェアハウスアプライアンス用の System Center 監視パック](https://go.microsoft.com/fwlink/p/?LinkId=282661)をダウンロードしてください。  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="Step2"></a>手順 2. 管理パックをインストールする  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>SQL Server アプライアンスベース管理パックをインストールする  
  
1.  インストールを実行するには、ダウンロードした SQL Server アプライアンスベース管理パックをダブルクリックします。  
  
2.  使用許諾契約書に同意し、[**次へ**] をクリックします。  
  
    ![使用許諾契約書に同意する](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  独自のインストールフォルダーを選択するか、既定の管理パックのインストールフォルダーを使用します。  
  
    ![インストール先フォルダーの選択](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  
  **[インストール]** をクリックします。  
  
    ![インストールの確認](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  [**閉じる**] をクリックします。  
  
    ![[閉じる] をクリックしてください](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>SQL Server PDW アプライアンス用監視パックのインストール  
  
1.  インストールを実行するには、ダウンロードした SQL Server PDW アプライアンス管理パックをダブルクリックします。  
  
2.  使用許諾契約書に同意し、[**次へ**] をクリックします。  
  
    ![使用許諾契約に同意](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  抽出されたファイルを保持するディレクトリを選択します。 既定では、既定の管理パックのインストールフォルダーが表示されます。 既定値を選択するか、独自のインストールフォルダーを選択します。  
  
    ![インストール先フォルダーの選択](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  
  **[インストール]** をクリックします。  
  
    ![インストールの確認](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  [**閉じる**] をクリックします。  
  
    ![インストールの完了](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>次のステップ  
管理パックがインストールされたので、次の手順「 [PDW 用の SCOM 管理パックをインポートする &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md)」に進みます。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
