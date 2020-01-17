---
title: エクスポート前のデータのフィルター処理 (Excel 用 MDS アドイン) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 58887c2e1590631b4d80cad0191a2bb9158e5b68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092364"
---
# <a name="filter-data-before-exporting-mds-add-in-for-excel"></a>エクスポート前のデータのフィルター処理 (Excel 用 MDS アドイン)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] で、Excel にエクスポートするデータのサイズまたはスコープを制限するには、データをフィルター処理します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
### <a name="to-filter-data-before-exporting"></a>エクスポート前のデータをフィルター処理するには  
  
1.  Excel を開いて、 **[マスター データ]** タブで MDS リポジトリに接続します。 詳細については、「[MDS リポジトリへの接続 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)」を参照してください。  
  
2.  **[マスター データ エクスプローラー]** ペインで、モデルおよびバージョンを選択します。 エンティティの一覧が作成されます。  
  
    -   **[マスター データ エクスプローラー]** ペインが表示されない場合は、 **[接続と読み込み]** グループの **[エクスプローラーの表示]** をクリックします。  
  
    -   **[マスター データ エクスプローラー]** ペインが無効になっている場合は、既存のシートに MDS によって管理されるデータが既に含まれています。 ペインを有効にするには、新しいワークシートを開きます。  
  
3.  **[マスター データ エクスプローラー]** ペインのエンティティの一覧で、フィルター処理するエンティティをクリックします。  
  
4.  リボンの **[接続と読み込み]** グループで、 **[フィルター]** をクリックします。  
  
5.  **[フィルター]** ダイアログ ボックスで、表示する属性 (列) を選択して列の順序を設定し、必要に応じて、返される行が少なくなるようにデータをフィルター処理します。 **[概要]** ペインで、返されるデータ量を確認します。 詳細については、「[[フィルター] ダイアログ ボックス (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)」を参照してください。  
  
6.  **[データの読み込み]** をクリックします。 シートに MDS によって管理されるデータが入力されます。  
  
    > [!NOTE]  
    >  -   最初の 100 万個のメンバーだけが Excel に読み込まれます。  
    > -   制約リスト (ドメイン ベースの属性) の列では、既定で最初の 25,000 個の値だけが読み込まれます。  
  
## <a name="next-steps"></a>次の手順  
 [Excel からマスター データ サービスにデータをインポートする (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>関連項目  
 [概要:データを Excel にエクスポートする&#40;MDS アドインの Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [[フィルター] ダイアログ ボックス (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [列の並べ替え (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  
