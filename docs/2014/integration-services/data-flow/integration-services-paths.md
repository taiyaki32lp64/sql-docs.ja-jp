---
title: Integration Services のパス | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 832ea48478eb28b94caf292067344a3754040b2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901796"
---
# <a name="integration-services-paths"></a>Integration Services のパス
  パスは、データ フロー コンポーネントの出力を別のコンポーネントの入力に連結することにより、データ フロー内の 2 つのコンポーネントを連結します。 パスには連結元と連結先があります。 たとえば、パスが OLE DB ソースと並べ替え変換を連結する場合、OLE DB ソースはパスの連結元であり、並べ替え変換はパスの連結先になります。 連結元とはパスが開始するコンポーネントで、連結先とはパスが終了するコンポーネントのことです。  
  
 パッケージを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで実行する場合、データ ビューアーをパスにアタッチすることにより、データ フロー内のデータを表示できます。 データ ビューアーを構成し、グリッドにデータを表示できます。 データ ビューアーは、デバッグ用のツールとして便利です。 詳細については、「 [データ フローのデバッグ](../troubleshooting/debugging-data-flow.md)」を参照してください。  
  
## <a name="configuration-of-the-path"></a>パスの構成  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは **[データ フロー パス エディター]** ダイアログ ボックスが用意され、これを使用すると、パスのプロパティの設定、パスに渡されるデータ列のメタデータの表示、およびデータ ビューアーの構成を行うことができます。  
  
 構成可能なパスのプロパティは、パスの名前、説明、および注釈です。 パスはプログラムによって構成することもできます。 詳細については、「 [プログラムによるデータ フロー コンポーネントの接続](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)」を参照してください。  
  
 パスの注釈を設定すると、 **デザイナーの** [データ フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブにあるデザイン画面に、パスの連結元の名前またはパスの名前が表示されます。 パスの注釈は、データ フロー、制御フロー、およびイベント ハンドラーに追加できる注釈と同様です。 唯一の違いは、パスの注釈はパスにアタッチされるのに対し、他の注釈は、 **デザイナーの**[データ フロー] **、** [制御フロー] **、および**[イベント ハンドラー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブに表示される点です。  
  
 パスの注釈のメタデータは、各列の名前、データ型、有効桁数、小数点以下桁数、長さ、コード ページ、およびソース コンポーネントを、直前のコンポーネントの出力内で表示します。 ソース コンポーネントとは、列を作成したデータ フロー コンポーネントのことです。 このコンポーネントは、データ フロー内で最初のコンポーネントである場合もあれば、そうでない場合もあります。 たとえば、全体結合変換と並べ替え変換では独自の列が作成され、その列が出力列のソースになります。 対照的に、列コピー変換では、列を変更しないまま渡したり、入力列をコピーして新しい列を作成できます。 列コピー変換は、新しい列に対してのみ変換元コンポーネントとなります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[データ フロー パス エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー パス エディター &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [データ フロー パス エディター&#40;メタデータ ページ&#41;](../data-flow-path-editor-metadata-page.md)  
  
-   [データ フロー パス エディター&#40;データ ビューアー ページ&#41;](../data-flow-path-editor-data-viewers-page.md)  
  
 プログラムによって設定できるプロパティの詳細については、「[パスのプロパティ](../path-properties.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [データ フロー パス エディターでパスのメタデータを表示する](../view-path-metadata-in-the-data-flow-path-editor.md)  
  
-   [データ フロー内でコンポーネントを連結する](connect-components-in-a-data-flow.md)  
  
## <a name="see-also"></a>参照  
 [データ フロー](data-flow.md)  
  
  
