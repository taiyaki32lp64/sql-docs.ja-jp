---
title: 一般的に使用されるフィルター (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- multivalued parameters [Reporting Services]
- single-valued parameters [Reporting Services]
- parameters [Reporting Services], multivalued
- valid values [Reporting Services]
ms.assetid: cb70d0cd-707b-4de5-b39f-e4eb57d316aa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f807060994c2225dc1e6605344bbb3bd5d2709e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106242"
---
# <a name="commonly-used-filters-report-builder-and-ssrs"></a>一般的に使用されるフィルター (レポート ビルダーおよび SSRS)
  フィルターを作成するには、1 つ以上のフィルター式を指定する必要があります。 フィルター式には、式、データ型、演算子、および値が含まれます。 ここでは、一般的に使用されるフィルターの例を示します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>フィルターの例  
 次の表は、さまざまなデータ型と演算子を使用するフィルター式の例を示します。 比較のスコープは、フィルターが定義されたレポート アイテムによって決まります。 たとえば、データセットに定義されたフィルターの場合、 **[上位 10%]** はデータセットの値の上位 10% になります。グループに定義されたフィルターの場合、 **[上位 10%]** はグループの値の上位 10% になります。  
  
|単純式|データ型|演算子|値|説明|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|`Integer`|`>`|`7`|7 より大きいデータ値が含まれます。|  
|`[SUM(Quantity)]`|`Integer`|`TOP N`|`10`|上位 10 データ値が含まれます。|  
|`[SUM(Quantity)]`|`Integer`|`TOP %`|`20`|上位 20% のデータ値が含まれます。|  
|`[Sales]`|`Text`|`>`|`=CDec(100)`|$100 より大きい System.Decimal 型 (SQL "money" データ型) のすべての値が含まれます。|  
|`[OrderDate]`|`DateTime`|`>`|`2088-01-01`|2008 年 1 月 1 日から現在の日付までのすべての日付が含まれます。|  
|`[OrderDate]`|`DateTime`|`BETWEEN`|`2008-01-01`<br /><br /> `2008-02-01`|2008 年 1 月 1 日から 2008 年 2 月 1 日までの日付が含まれます。|  
|`[Territory]`|`Text`|`LIKE`|`*east`|最後に "east" が付くすべての販売区域名。|  
|`[Territory]`|`Text`|`LIKE`|`%o%th*`|名前の先頭に North と South が含まれるすべての販売区域名。|  
|`=LEFT(Fields!Subcat.Value,1)`|`Text`|`IN`|`B, C, T`|B、C、T のいずれかの文字で始まるすべてのサブカテゴリ値。|  
  
## <a name="examples-with-report-parameters"></a>レポート パラメーターの例  
 次の表は、単一値か複数値のパラメーター参照を含むフィルター式の例を示します。  
  
|パラメーターの型|(フィルター) 式|演算子|値|データ型|  
|--------------------|---------------------------|--------------|-----------|---------------|  
|単一値|`[EmployeeID]`|=|`[@EmployeeID]`|Integer|  
|MultiValue|`[EmployeeID]`|IN|`[@EmployeeID]`|Integer|  
  
## <a name="see-also"></a>関連項目  
 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](report-parameters-report-builder-and-report-designer.md)   
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
