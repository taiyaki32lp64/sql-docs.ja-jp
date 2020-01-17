---
title: 列の並べ替え (Excel 用 MDS アドイン) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6002b634c38d40f9446bb7facc087fb0eef462ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074429"
---
# <a name="reorder-columns-mds-add-in-for-excel"></a>列の並べ替え (Excel 用 MDS アドイン)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] では、読み込み前に一覧をフィルター処理して列を並べ替えることができます。  
  
 **[フィルター]** ダイアログ ボックスの属性を並べ替えると、Excel には新しい順序でデータが読み込まれます。 しかし、次にその属性データをフィルター処理すると、元のデザインの順序に戻ります。 順序を完全に変更するには、管理者がマスター データ マネージャーの **[システム管理]** 領域で順序を変更する必要があります。 詳細については、「 [Change the Order of Attributes](../../master-data-services/change-the-order-of-attributes.md)」を参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
### <a name="to-reorder-mds-managed-columns"></a>MDS によって管理される列を並べ替えるには  
  
1.  Excel を開いて、 **[マスター データ]** タブで MDS リポジトリに接続します。 詳細については、「[MDS リポジトリへの接続 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)」を参照してください。  
  
2.  **[マスター データ エクスプローラー]** ペインで、モデルおよびバージョンを選択します。 エンティティの一覧が作成されます。  
  
    -   **[マスター データ エクスプローラー]** ペインが表示されない場合は、 **[接続と読み込み]** グループの **[エクスプローラーの表示]** をクリックします。  
  
    -   **[マスター データ エクスプローラー]** ペインが無効になっている場合は、既存のシートに MDS によって管理されるデータが既に含まれています。 ペインを有効にするには、新しいワークシートを開きます。  
  
3.  **[マスター データ エクスプローラー]** ペインで、エンティティをクリックします。  
  
4.  **[接続と読み込み]** グループで、 **[フィルター]** をクリックします。  
  
5.  **[フィルター]** ダイアログ ボックスの **[列]** セクションに表示される属性の一覧で、移動する属性をクリックします。  
  
6.  一覧の右側で、 **上** 矢印または **下** 矢印をクリックして、ワークシート内の属性を左右に移動します。  
  
7.  ワークシート内で目的の順序 (左から右) となるまで、各属性について手順 7. を繰り返します。  
  
8.  **[データの読み込み]** をクリックします。 MDS によって管理されるデータがシートに入力され、指定した順序で列が表示されます。  
  
## <a name="see-also"></a>関連項目  
 [概要:Excel へのデータのエクスポート &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
