---
title: (MDS アドインを Excel 用) を読み込む前にデータをフィルター処理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 277b5ff1e575f223b78f958e26801e7b209d05d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478931"
---
# <a name="filter-data-before-loading-mds-add-in-for-excel"></a>読み込み前のデータのフィルター処理 (Excel 用 MDS アドイン)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]、サイズまたは Excel に読み込むデータのスコープを制限する場合に、データをフィルター処理します。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
### <a name="to-filter-data-before-loading"></a>読み込み前にデータをフィルター処理するには  
  
1.  Excel を開いて、 **[マスター データ]** タブで MDS リポジトリに接続します。 詳細については、「[MDS リポジトリへの接続 (Excel 用 MDS アドイン)](connect-to-an-mds-repository-mds-add-in-for-excel.md)」を参照してください。  
  
2.  **[マスター データ エクスプローラー]** ペインで、モデルおよびバージョンを選択します。 エンティティの一覧が作成されます。  
  
    -   **[マスター データ エクスプローラー]** ペインが表示されない場合は、 **[接続と読み込み]** グループの **[エクスプローラーの表示]** をクリックします。  
  
    -   **[マスター データ エクスプローラー]** ペインが無効になっている場合は、既存のシートに MDS によって管理されるデータが既に含まれています。 ペインを有効にするには、新しいワークシートを開きます。  
  
3.  **[マスター データ エクスプローラー]** ペインのエンティティの一覧で、フィルター処理するエンティティをクリックします。  
  
4.  リボンの **[接続と読み込み]** グループで、 **[フィルター]** をクリックします。  
  
5.  **[フィルター]** ダイアログ ボックスで、表示する属性 (列) を選択して列の順序を設定し、必要に応じて、返される行が少なくなるようにデータをフィルター処理します。 **[概要]** ペインで、返されるデータ量を確認します。 詳細については、「[[フィルター] ダイアログ ボックス (Excel 用 MDS アドイン)](filter-dialog-box-mds-add-in-for-excel.md)」を参照してください。  
  
6.  **[データの読み込み]** をクリックします。 シートに MDS によって管理されるデータが入力されます。  
  
    > [!NOTE]  
    >  -   最初の 100 万個のメンバーだけが Excel に読み込まれます。  
    > -   制約付き一覧 (ドメイン ベースの属性) である列の場合は、最初の 1000 個の値のみが読み込まれます。  
  
## <a name="next-steps"></a>次の手順  
 [Excel からデータを MDS にパブリッシュ&#40;MDS アドインの Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>参照  
 [データの読み込み&#40;MDS アドインの Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [[フィルター] ダイアログ ボックス (Excel 用 MDS アドイン)](filter-dialog-box-mds-add-in-for-excel.md)   
 [列の並べ替え (Excel 用 MDS アドイン)](reorder-columns-mds-add-in-for-excel.md)  
  
  
