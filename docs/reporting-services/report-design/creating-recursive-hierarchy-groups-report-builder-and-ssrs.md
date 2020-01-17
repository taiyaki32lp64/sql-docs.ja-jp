---
title: 複数の再帰型階層グループの作成 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9125adcb007e7f191ab30bc0b957580d0012e859
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581516"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>複数の再帰型階層グループの作成 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートに再帰型データを表示するには (親子間のリレーションシップがデータセットのフィールドで表されている)、子フィールドに基づいたデータ領域グループ式や、親フィールドに基づいた親プロパティを設定できます。  
  
 階層データの表示は、組織図に含まれている従業員など、再帰型階層グループでよく使用されます。 データセットには従業員とマネージャーの一覧が含まれており、マネージャー名は従業員の一覧にも表示されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>再帰型階層の作成  
 Tablix データ領域で再帰型階層を作成するには、子データを指定するフィールドにグループ式を設定し、親データを指定するフィールドにグループの親プロパティを設定する必要があります。 たとえば、従業員がマネージャーの監督下にある場合、従業員 ID およびマネージャー ID のフィールドを含んでいるデータセットでは、グループ式を従業員 ID に設定し、親プロパティをマネージャー ID に設定します。  
  
 再帰型階層として定義されたグループ (親プロパティを使用しているグループ) には、グループ式は 1 つしか設定できません。 テキスト ボックスの余白に **Level** 関数を使用して、階層内のレベルに応じて従業員名をインデントできます。  
  
 詳細については、「[データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」と「[再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="aggregate-functions-that-support-recursion"></a>再帰をサポートする集計関数  
 パラメーター *Recursive* を受け取る Reporting Services 集計関数を使用して、再帰型階層の集計データを計算できます。 関数 **Sum** 、 [Avg](../../reporting-services/report-design/report-builder-functions-sum-function.md)、 [Count](../../reporting-services/report-design/report-builder-functions-avg-function.md)、 [CountDistinct](../../reporting-services/report-design/report-builder-functions-count-function.md)、 [CountRows](../../reporting-services/report-design/report-builder-functions-countdistinct-function.md)、 [Max](../../reporting-services/report-design/report-builder-functions-countrows-function.md)、 [Min](../../reporting-services/report-design/report-builder-functions-max-function.md)、 [StDev](../../reporting-services/report-design/report-builder-functions-min-function.md)、 [StDevP](../../reporting-services/report-design/report-builder-functions-stdev-function.md)、 [Sum](../../reporting-services/report-design/report-builder-functions-stdevp-function.md)、 [Var](../../reporting-services/report-design/report-builder-functions-sum-function.md)、 [VarP](../../reporting-services/report-design/report-builder-functions-var-function.md)は、パラメーターとして [Recursive](../../reporting-services/report-design/report-builder-functions-varp-function.md)を受け入れます。 詳細については、「 [集計関数リファレンス (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [集計関数リファレンス (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)    
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
