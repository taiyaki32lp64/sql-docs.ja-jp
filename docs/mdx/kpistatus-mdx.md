---
title: KPIStatus (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aa07788bc00cc3317024d287f1054a67c6447356
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905881"
---
# <a name="kpistatus-mdx"></a>KPIStatus (MDX)


  指定された主要業績評価指標 (KPI) の [状態] 領域を表す正規化された値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
KPIStatus(KPI_Name)  
```  
  
## <a name="arguments"></a>引数  
 *Kpi 名*  
 KPI の名前を指定する有効な文字列式。  
  
## <a name="remarks"></a>コメント  
 状態値は-1 ~ 1 の正規化された値では一般にします。  
  
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
  
  
