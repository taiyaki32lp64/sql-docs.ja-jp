---
title: "マルチキャスト変換 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.multicasttrans.f1
- sql13.dts.designer.multicasttransformation.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: bd3eee42fbb204a9ca1e806d273b7c09a86c87d2
ms.contentlocale: ja-jp
ms.lasthandoff: 08/19/2017

---
# <a name="multicast-transformation"></a>マルチキャスト変換
  マルチキャスト変換は、入力を 1 つ以上の出力に配信します。 この変換は条件分割変換と似ています。 いずれの変換も、1 つの入力を複数の出力に送信します。 この 2 つの変換の違いは、マルチキャスト変換は各行を各出力に送信するのに対し、条件分割変換は 1 行を単一の出力に送信する点です。 詳細については、「 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)」を参照してください。  
  
 マルチキャスト変換を構成するには、出力を追加します。  
  
 マルチキャスト変換を使用すると、パッケージはデータの論理コピーを作成できます。 この機能は、パッケージで複数の変換セットを同一のデータに適用する必要がある場合に役に立ちます。 たとえば、データの 1 つのコピーを集計して要約情報のみを変換先で読み込み、そのデータのもう 1 つのコピーを参照値と派生列で拡張し、その後変換先で読み込みます。  
  
 この変換は 1 つの入力と複数の出力をとります。 エラー出力はサポートされていません。  
  
## <a name="configuration-of-the-multicast-transformation"></a>マルチキャスト変換の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 プログラムによって設定できるプロパティの詳細については、「 [共通プロパティ](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)」を参照してください。  
  
## <a name="related-tasks"></a>関連タスク  
 このコンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="multicast-transformation-editor"></a>マルチキャスト変換エディター
  **[マルチキャスト変換エディター]** ダイアログ ボックスを使用すると、各変換出力のプロパティを表示したり設定したりできます。  
  
### <a name="options"></a>オプション  
 **出力**  
 左側で出力を選択すると、右側の表にプロパティが表示されます。  
  
 **プロパティ**  
 表示されている出力プロパティの **[名前]** および **[説明]**以外はすべて読み取り専用です。  
  
## <a name="see-also"></a>参照  
 [データ フロー](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  