---
title: '[式] ページ | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9e3bbe6e788512144211ed35d1cfa8326d8f3ef7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290014"
---
# <a name="expressions-page"></a>[式] ページ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[式]** ページを使用すると、プロパティ式を編集でき、 **[プロパティ式エディター]** ダイアログ ボックスや **[式ビルダー]** ダイアログ ボックスにアクセスできます。  
  
 プロパティ式は、パッケージが実行されたときに、プロパティの値を更新します。 プロパティ式は、パッケージ、タスク、コンテナー、接続マネージャーに加えて、一部のデータ フロー コンポーネントのプロパティでも使用できます。 式が評価されると、その結果が、パッケージおよびパッケージ オブジェクトの構成時にプロパティに設定した値の代わりに使用されます。 式には、変数と、式の言語で提供されている関数および演算子を含めることができます。 たとえば、文字列 "Weather forecast for " を含む変数の値と、GETDATE() 関数によって返される結果を連結して、文字列 "Weather forecast for 4/5/2006" を作成することにより、メール送信タスクの件名行を生成することができます。  
  
 式の作成とプロパティ式の使用の詳細については、「 [Integration Services &#40;SSIS&#41; 式](../../integration-services/expressions/integration-services-ssis-expressions.md) ダイアログ ボックスや [パッケージでプロパティ式を使用する](../../integration-services/expressions/use-property-expressions-in-packages.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **式 (...)**  
 [...] をクリックすると、 **[プロパティ式エディター]** ダイアログ ボックスが表示されます。 詳細については、「 [プロパティ式エディター](../../integration-services/expressions/property-expressions-editor.md)」を参照してください。  
  
 **\<プロパティ名>**  
 [...] をクリックすると、 **[式ビルダー]** ダイアログ ボックスが表示されます。 詳細については、「 [式ビルダー](../../integration-services/expressions/expression-builder.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)   
 [システム変数](../../integration-services/system-variables.md)   
 [Integration Services &#40;SSIS&#41; 式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
