---
title: "MDS リポジトリ (MDS アドインを Excel 用) への接続 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
caps.latest.revision: 12
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 87931c60b791fd106d0476ac037e1dfcd4041fb2
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>MDS リポジトリへの接続 (Excel 用 MDS アドイン)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]では、データの読み込みまたはパブリッシュの前に MDS リポジトリに接続する必要があります。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
### <a name="to-connect-to-an-mds-repository"></a>MDS リポジトリに接続するには  
  
1.  MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]の **[マスター データ]** タブの **[接続と読み込み]** グループで、 **[接続]** ボタンの下の矢印をクリックし、 **[接続の管理]**をクリックします。  
  
2.  **[接続の管理]** ダイアログ ボックスの **[新しい接続]** セクションで、 **[新しい接続の作成]**をクリックします。  
  
3.  **[新規作成]**をクリックします。  
  
4.  **[新しい接続の追加]** ダイアログ ボックスの **[説明]** フィールドに、接続の説明を入力します。 この接続は、ツール バーの **[接続]** ボタンの下の矢印をクリックしたときに表示されます。  
  
5.  **MDS サーバー アドレス**ボックスの URL を入力、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] web アプリケーション、たとえば`http://contoso/mds`します。  
  
    > [!NOTE]  
    >  必ずコンピューター名を使用してください。"localhost" を使用しないでください。  
  
6.  **[OK]**をクリックします。 **[既存の接続]** セクションに名前が表示されます。  
  
7.  必要であれば、 **[テスト]** をクリックして接続をテストします。 確認ダイアログまたはエラー ダイアログが表示されます。 **[OK]** をクリックして閉じます。  
  
8.  **[接続]**をクリックします。 **[マスター データ サービス]** ペインが表示されます。  
  
## <a name="next-steps"></a>次の手順  
  
-   [マスター データ サービスから Excel へのデータのエクスポート](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)  
  
-   [エクスポート前のデータのフィルター処理 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>参照  
 [接続 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
  