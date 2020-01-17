---
title: ストアド プロシージャ (MDX) の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4daa38f185569e1579413870cc929a8b1b3b6570
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038007"
---
# <a name="using-stored-procedures-mdx"></a>ストアド プロシージャの使用 (MDX)


  .NET ストアド プロシージャやユーザー定義関数を記述して [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] および多次元式 (MDX) の機能を拡張できます。 詳細については、次を参照してください[ADOMD.NET サーバー プログラミング。](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
 参照するか、またはストアド プロシージャを呼び出すときに、関数名の後にかっこを指定します。 かっこの中には、パラメーターに渡されるデータを提供する引数と呼ばれる式を指定できます。 関数を呼び出すときに、パラメーターのすべての引数の値を指定する必要があり、パラメーターが、ユーザー定義関数で定義されている同じ順序で引数の値を指定する必要があります。  
  
 次のクエリでは、SampleAssembly という名前のアセンブリが [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] サーバーに登録されていることを前提としています。  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
> [!NOTE]  
>  *ストアド プロシージャ*で使用される用語は、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のこれらの種類の関数。 以前のバージョンの[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]関数としてのこれらの型と呼ばれる*ユーザー定義関数*します。  
  
## <a name="types-of-stored-procedures"></a>ストアド プロシージャの種類  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は COM アセンブリと CLR アセンブリの両方をサポートします。 CLR アセンブリは CLR アセンブリを使用可能なセキュリティの強化のためお勧めします。 サーバーに Microsoft Office Excel がインストールされている場合、Excel 関数も使用可能です。  
  
> [!NOTE]  
>  Microsoft Visual Basic for Applications (VBA) COM アセンブリは自動的に登録されます。  
  
## <a name="see-also"></a>関連項目  
 [関数&#40;MDX 構文&#41;](../mdx/functions-mdx-syntax.md)  
  
  
