---
title: XSINIL パラメーターを使用した NULL 値に対する要素の生成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d056959f5e05d3de79fa81d33331390f4decb49a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205606"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>XSINIL パラメーターを使用した NULL 値に対する要素の生成
  **ELEMENTS** ディレクティブにより構成される XML では、各列の値が XML の要素にマップされます。 列の値が NULL の場合、要素は追加されません。 ELEMENTS ディレクティブでオプションの **XSINIL** パラメーターを指定すると、NULL 値に対しても要素を作成するように要求できます。 この場合、値が NULL の各列に対して、TRUE に設定された **xsi:nil** 属性を持つ要素が返されます。  
  
## <a name="see-also"></a>参照  
 [FOR XML での RAW モードの使用](use-raw-mode-with-for-xml.md)  
  
  
