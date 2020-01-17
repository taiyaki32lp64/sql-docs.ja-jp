---
title: エラー処理 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 611e7636f9a5cd6393da4a8412b6c02bcc9ddaf8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074676"
---
# <a name="error-handling-mdx"></a>エラー処理 (MDX)
  各キューブでは、多次元式 (MDX) スクリプト内のエラーの処理方法を制御できます。 エラー処理は `ScriptErrorHandlingMode` 列挙子を使用して行われます。 この列挙子は、以下のいずれかの値をとります。  
  
 `IgnoreNone`  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] が MDX スクリプト内になんらかのエラーを検出した場合、サーバーはエラーを生成します。  
  
 `IgnoreAll`  
 サーバーは、MDX スクリプト内のエラー (構文エラー、名前の解決エラーなど) を含むすべてのコマンドを無視します。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
