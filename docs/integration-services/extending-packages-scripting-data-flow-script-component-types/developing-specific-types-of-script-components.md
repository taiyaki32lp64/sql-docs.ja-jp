---
title: 特定の種類のスクリプト コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d98a0a0293114e1b701ecd90f4a7b1ab058b0aa4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296406"
---
# <a name="developing-specific-types-of-script-components"></a>特定の種類のスクリプト コンポーネントの開発

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  スクリプト コンポーネントは構成可能なツールです。パッケージのデータ フローで使用すると、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に備わっている変換元、変換、および変換先では満たせないほとんどすべての要件に対応できます。 ここで紹介するスクリプト コンポーネントのコード例では、スクリプト コンポーネントの 4 つの構成方法を説明します。  
  
-   変換元として構成する  
  
-   同期出力型の変換として構成する  
  
-   非同期出力型の変換として出力する  
  
-   変換先として出力する  
  
 スクリプト コンポーネントのその他の例については、「[その他のスクリプト コンポーネントの例](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [スクリプト コンポーネントによる変換元の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)  
 スクリプト コンポーネントを使用してデータ フローの変換元を作成する方法を、説明および例示します。  
  
 [スクリプト コンポーネントによる同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 スクリプト コンポーネントを使用して同期出力型のデータ フロー変換を作成する方法を、説明および例示します。 この種類の変換は、スクリプト コンポーネントを通過する時点でデータ行を変更します。  
  
 [スクリプト コンポーネントによる非同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 スクリプト コンポーネントを使用して非同期出力型のデータ フロー変換を作成する方法を、説明および例示します。 この種類の変換では、計算された集計結果などの追加情報をコンポーネントを通過するデータに追加する前に、すべてのデータ行を読み取る必要があります。  
  
 [スクリプト コンポーネントによる変換先の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 スクリプト コンポーネントを使用してデータ フローの変換先を作成する方法を、説明および例示します。  
  
## <a name="see-also"></a>参照  
 [スクリプティング ソリューションとカスタム オブジェクトとの比較](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [特定の種類のデータ フロー コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  
