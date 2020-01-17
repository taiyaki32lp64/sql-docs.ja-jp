---
title: 詳細グループの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ef8efba-6d48-4aeb-a3b9-a02ba5a44614
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe6fffc96a816c9b71c003926d6267e8287a1c48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106854"
---
# <a name="add-a-details-group-report-builder-and-ssrs"></a>詳細グループの追加 (レポート ビルダーおよび SSRS)
  レポート データセットの詳細データは、グループ式のないグループとして指定されます。 マトリックスの詳細データを表示したり、表や一覧から削除した詳細データを再び追加したり、詳細グループを追加したりするときは、既存の Tablix データ領域に詳細グループを追加します。 グループの詳細については、「 [グループについて (レポート ビルダーおよび SSRS)](understanding-groups-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-details-group-to-a-tablix-data-region"></a>詳細グループを Tablix データ領域に追加するには  
  
1.  デザイン画面で、Tablix データ領域の任意の場所をクリックして選択します。 グループ化ペインに、選択したデータ領域の行グループと列グループが表示されます。  
  
2.  [グループ化] ペインで、最も内側の子グループを右クリックします。 **[グループの追加]** をクリックし、 **[子グループ]** をクリックします。 **[Tablix のグループ]** ダイアログ ボックスが表示されます。  
  
3.  **[グループ式]** で式を空白のままにします。 詳細グループには式がありません。  
  
4.  **[詳細データの表示]** をクリックします。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     グループ化ペインで新しい詳細グループが子グループとして追加され、手順 1. で選択したグループの行ハンドルに詳細グループ アイコンが表示されます。 Tablix データ領域に関する詳細については、「[Tablix データ領域のセル、行、および列 &#40;レポート ビルダーおよび SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ領域でのグループの追加または削除 (レポート ビルダーおよび SSRS)](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [グループについて (レポート ビルダーおよび SSRS)](understanding-groups-report-builder-and-ssrs.md)   
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
