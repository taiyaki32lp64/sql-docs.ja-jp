---
title: ピボット解除変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 98a8476ef317a0ddfa6f7fc27c0c9572ed12817a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770197"
---
# <a name="unpivot-transformation"></a>ピボット解除変換
  ピボット解除変換は、単一のレコード内にある複数の列の値を、単一の列内で同じ値を持つ複数のレコードに展開することにより、正規化されていないデータセットを正規化されたバージョンに変換します。 たとえば、顧客名を一覧表示するデータセットに、顧客ごとに 1 つの行があり、製品と購入した数量がその行の列に表示されているとします。 ピボット解除変換がこのデータセットを正規化すると、データセットには、顧客が購入した各製品に対して異なる行が含まれるようになります。  
  
 次の図は、データが Product 列でピボット解除される前のデータセットを示しています。  
  
 ![ピボット解除後のデータセット](../../media/mw-dts-18.gif "ピボット解除後のデータセット")  
  
 次の図は、データが Product 列でピボット解除された後のデータセットを示しています。  
  
 ![ピボット解除前のデータセット](../../media/mw-dts-17.gif "ピボット解除前のデータセット")  
  
 状況によっては、ピボット解除された結果には予期しない値を持つ行が含まれる場合があります。 たとえば、図に示したサンプル データのピボット解除では、Fred のすべての Qty 列が NULL 値である場合、出力に含まれる Fred の行は 5 つではなく 1 つだけです。 Qty 列には、列データ型に応じて、NULL または 0 のいずれかが含まれます。  
  
## <a name="configuration-of-the-unpivot-transformation"></a>ピボット解除変換の構成  
 ピボット解除変換には、`PivotKeyValue` カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../../expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../expressions/use-property-expressions-in-packages.md)」、および「[変換のカスタム プロパティ](transformation-custom-properties.md)」を参照してください。  
  
 この変換は 1 つの入力と 1 つの出力をとります。 エラー出力はありません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[ピボット解除変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[ピボット解除変換エディター]](../../unpivot-transformation-editor.md)  
  
 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
  
