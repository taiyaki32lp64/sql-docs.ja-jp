---
title: KPITrend (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 26e33a84ff50fca00151dc124403bac9daa2d89d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905860"
---
# <a name="kpitrend-mdx"></a>KPITrend (MDX)


  指定された主要業績評価指標 (KPI) の傾向を表す正規化された値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
KPITrend(KPI_Name)  
```  
  
## <a name="arguments"></a>引数  
 *Kpi 名*  
 KPI の名前を指定する有効な文字列式。  
  
## <a name="remarks"></a>コメント  
 傾向値は、一般に、-1 ~ 1 の間の正規化された値です。  
  
## <a name="example"></a>例  
 次の例では、KPI の値、KPI 目標、KPI の状態、および、Fiscal Year 属性階層の 3 つのメンバーの子孫に対する、channel revenue メジャーの KPI の傾向を返します。  
  
```  
SELECT  
   { KPIValue("Channel Revenue"),   
     KPIGoal("Channel Revenue"),  
     KPIStatus("Channel Revenue"),   
     KPITrend("Channel Revenue")  
   } ON Columns,  
Descendants  
   ( { [Date].[Fiscal].[Fiscal Year].&[2002],  
       [Date].[Fiscal].[Fiscal Year].&[2003],  
       [Date].[Fiscal].[Fiscal Year].&[2004]   
     }, [Date].[Fiscal].[Fiscal Quarter]  
   ) ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
