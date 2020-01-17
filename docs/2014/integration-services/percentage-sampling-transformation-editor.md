---
title: 比率サンプリング変換エディター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- Percentage Sampling Transformation Editor
ms.assetid: 2c40d804-26a3-4d35-809b-bc923d83d451
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0366ecb08281a28d43bc98639bf4b11e60aea402
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056720"
---
# <a name="percentage-sampling-transformation-editor"></a>比率サンプリング変換エディター
  **[比率サンプリング変換エディター]** ダイアログ ボックスを使用すると、指定された行の割合を使用して、入力の一部をサンプルに分割できます。 この変換は、入力を 2 つの別個の出力に分割します。  
  
 比率サンプリング変換の詳細については、「 [Percentage Sampling Transformation](data-flow/transformations/percentage-sampling-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[行の割合]**  
 サンプルとして使用する入力における行の割合を指定します。  
  
 このプロパティの値は、プロパティ式を使用して指定することができます。  
  
 **[サンプル出力名]**  
 サンプリングされた行を含める出力の一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **[選択されていない出力名]**  
 サンプリングから除外された行を含む出力の一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **[次のランダム シードを使用する]**  
 変換でサンプルを作成するために使用する乱数ジェネレーターのサンプリング シードを指定します。 このオプションは、開発およびテスト用にのみ使用することをお勧めします。 ランダム シードが指定されない場合は、Microsoft Windows のティック数が使用されます。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [行サンプリング変換](data-flow/transformations/row-sampling-transformation.md)  
  
  
