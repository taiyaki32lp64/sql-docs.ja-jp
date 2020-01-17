---
title: フラット ファイル変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledest.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 30f8f566dc04726076dd9eb7c4d91b56f687218d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62902464"
---
# <a name="flat-file-destination"></a>フラット ファイル変換先
  フラット ファイル変換先は、データをテキスト ファイルに書き込みます。 テキスト ファイルには、区切り形式、固定幅形式、行区切り記号を使用した固定幅形式、または幅合わせしない形式を使用できます。  
  
 フラット ファイル変換先は、次の方法で構成できます。  
  
-   データが書き込まれる前にファイルに挿入される、テキストのブロックを指定します。 このテキストには、列見出しなどの情報を設定できます。  
  
-   同じ名前の変換先ファイルにあるデータを上書きするかどうかを指定します。  
  
 この変換先では、フラット ファイル接続マネージャーを使用してテキスト ファイルにアクセスします。 フラット ファイル変換先が使用するフラット ファイル接続マネージャーでプロパティを設定することにより、フラット ファイル変換先がテキスト ファイルをフォーマットする方法と書き込む方法を指定できます。 フラット ファイル接続マネージャーを構成する際には、ファイルおよびファイル内の各列に関する情報を指定できます。 たとえば、ファイルの列と行を区切る文字や、各列のデータ型や長さを指定できます。 詳しくは、「 [フラット ファイル接続マネージャー](../connection-manager/file-connection-manager.md)」をご覧ください。  
  
 フラット ファイル変換先には、Header カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳しくは、「[Integration Services &#40;SSIS&#41; の式](../expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../expressions/use-property-expressions-in-packages.md)」、および「[フラット ファイルのカスタム プロパティ](flat-file-custom-properties.md)」をご覧ください。  
  
 この変換先は 1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="configuration-of-the-flat-file-destination"></a>フラット ファイル変換先の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[フラット ファイル ソース エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[フラット ファイル変換先エディター] &#40;[接続マネージャー] ページ&#41;](../flat-file-destination-editor-connection-manager-page.md)  
  
-   [[フラット ファイル変換先エディター] &#40;[マッピング] ページ&#41;](../flat-file-destination-editor-mappings-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [フラット ファイルのカスタム プロパティ](flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 データ フロー コンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [フラット ファイル ソース](flat-file-source.md)   
 [データ フロー](data-flow.md)  
  
  
