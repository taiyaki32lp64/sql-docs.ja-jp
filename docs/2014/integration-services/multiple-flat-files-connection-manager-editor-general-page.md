---
title: 複数フラット ファイル接続マネージャー エディター (全般 ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.general.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: 00129d43-2772-413b-bdf8-ac5de81cf4a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6d4b926d08096087735458ed309e5bc4189a87df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057482"
---
# <a name="multiple-flat-files-connection-manager-editor-general-page"></a>[複数フラット ファイル接続マネージャー エディター] ([全般] ページ)
  **[複数フラット ファイル接続マネージャー エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、同じデータ形式を持つファイルのグループを選択したり、そのデータ形式を指定したりできます。 複数フラット ファイル接続は、パッケージが同じ形式のテキスト ファイルのグループに接続できるようにします。  
  
 複数フラット ファイル接続マネージャーの詳細については、「 [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md)」を参照してください。  
  
## <a name="options"></a>および  
 **接続マネージャー名**  
 ワークフローにおける複数フラット ファイル接続の一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **[説明]**  
 接続の説明を記述します。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、接続の目的について記述することをお勧めします。  
  
 **ファイル名**  
 複数フラット ファイル接続で使用するパスおよびファイル名を入力します。 複数のファイルを指定するには、たとえば、"C:\\*.txt" のようにワイルドカード文字を使用するか、縦棒パイプ文字 (|) をファイル名の区切り文字として使用します。 すべてのファイルのデータ形式が同じである必要があります。  
  
 **[参照]**  
 複数フラット ファイル接続で使用するファイルの名前を参照します。 複数のファイルを選択できます。 すべてのファイルのデータ形式が同じである必要があります。  
  
 **ロケール**  
 場所を指定して、順序付けおよび日時の変換に関する情報を提供します。  
  
 **Unicode**  
 Unicode を使用するかどうかを示します。 Unicode を使用する場合は、コード ページを指定できません。  
  
 **コード ページ**  
 非 Unicode テキストのコード ページを指定します。  
  
 **形式**  
 区切り形式、固定幅形式、または幅合わせしない形式を使用するかどうかを示します。 すべてのファイルのデータ形式が同じである必要があります。  
  
|値|説明|  
|-----------|-----------------|  
|[区切り記号]|列は、 **[列]** ページで指定した区切り記号で区切られます。|  
|[固定幅]|列は、 **[列]** ページでマーカー ラインをドラッグして指定した幅に固定されます。|  
|[幅合わせしない]|幅合わせしないファイルとは、最後の列以外のすべての列が固定幅を持つファイルです。最後の列は、 **[列]** ページで指定した行区切り記号で区切られます。|  
  
 **テキスト修飾子**  
 使用するテキスト修飾子を指定します。 たとえば、テキストを引用符で囲むように指定できます。  
  
 **[ヘッダー行区切り記号]**  
 ヘッダー行の区切り記号の一覧から選択するか、区切り記号テキストを入力します。  
  
|値|説明|  
|-----------|-----------------|  
|**{CR}{LF}**|ヘッダー行は、復帰と改行の組み合わせで区切られます。|  
|**{CR}**|ヘッダー行は、復帰で区切られます。|  
|**{LF}**|ヘッダー行は、改行で区切られます。|  
|**[セミコロン {;}]**|ヘッダー行は、セミコロンで区切られます。|  
|**[コロン {:}]**|ヘッダー行は、コロンで区切られます。|  
|**[コンマ {,}]**|ヘッダー行は、コンマで区切られます。|  
|**[タブ {t}]**|ヘッダー行は、タブで区切られます。|  
|**[縦棒 {&#124;}]**|ヘッダー行は、縦棒で区切られます。|  
  
 **[スキップするヘッダー行数]**  
 必要に応じて、スキップするヘッダー行数を指定します。  
  
 **[先頭データ行を列名として使用する]**  
 先頭データ行を列名として使用するか、ここに列名を指定するかを示します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[複数フラット ファイル接続マネージャー エディター] &#40;[列] ページ&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [[複数フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [[複数フラット ファイル接続マネージャー エディター] &#40;[プレビュー] ページ&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
