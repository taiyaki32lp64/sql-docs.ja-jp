---
title: 特定の種類のスクリプト コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e0a811b88537d784c9e1db892003391914d50f5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62895182"
---
# <a name="developing-specific-types-of-script-components"></a>特定の種類のスクリプト コンポーネントの開発
  スクリプト コンポーネントは構成可能なツールです。パッケージのデータ フローで使用すると、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に備わっている変換元、変換、および変換先では満たせないほとんどすべての要件に対応できます。 ここで紹介するスクリプト コンポーネントのコード例では、スクリプト コンポーネントの 4 つの構成方法を説明します。  
  
-   変換元として構成する  
  
-   同期出力型の変換として構成する  
  
-   非同期出力型の変換として出力する  
  
-   変換先として出力する  
  
 スクリプト コンポーネントのその他の例については、「[その他のスクリプト コンポーネントの例](../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [スクリプト コンポーネントによる変換元の作成](creating-a-source-with-the-script-component.md)  
 スクリプト コンポーネントを使用してデータ フローの変換元を作成する方法を、説明および例示します。  
  
 [スクリプト コンポーネントによる同期変換の作成](creating-a-synchronous-transformation-with-the-script-component.md)  
 スクリプト コンポーネントを使用して同期出力型のデータ フロー変換を作成する方法を、説明および例示します。 この種類の変換は、スクリプト コンポーネントを通過する時点でデータ行を変更します。  
  
 [スクリプト コンポーネントによる非同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 スクリプト コンポーネントを使用して非同期出力型のデータ フロー変換を作成する方法を、説明および例示します。 この種類の変換では、計算された集計結果などの追加情報をコンポーネントを通過するデータに追加する前に、すべてのデータ行を読み取る必要があります。  
  
 [スクリプト コンポーネントによる変換先の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 スクリプト コンポーネントを使用してデータ フローの変換先を作成する方法を、説明および例示します。  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [スクリプティング ソリューションとカスタム オブジェクトとの比較](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [特定の種類のデータ フロー コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  
