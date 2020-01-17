---
title: '[フラット ファイル接続マネージャー エディター] ([詳細] ページ) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ffileconnection.columnproperties.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 58aa3dee-4774-4e0b-a956-96d199be4c3a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0e6e85161ea95a9494bbaf91338b4ddc559ecbf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058790"
---
# <a name="flat-file-connection-manager-editor-advanced-page"></a>[フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)
  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスの **[詳細設定]** ページでは、Integration Services で、フラット ファイルからデータをどのように読み取るか、フラット ファイルにデータをどのように書き込むかを指定するプロパティを設定できます。 フラット ファイル内の列名を変更し、ファイル内の各列にデータ型および区切り記号を指定するプロパティを設定できます。  
  
 既定では、文字列の列の長さは 50 文字です。 これらの列の長さを変更して、データが切り捨てられたり、列の幅が広くなりすぎないようにできます。 また、変換先列と互換性を持つように他のメタデータも更新できます。 たとえば、整数データのみを含む列のデータ型を、DT_I2 などの数値データ型に変更するなどの操作を行えます。 このような変更は手動で行えます。また、 **[型の選択]** ボタンをクリックし、 **[列の型の推測]** ダイアログ ボックスを使用して、サンプル データを評価し、自動的に変更することもできます。  
  
 フラット ファイル接続マネージャーの詳細については、「 [Flat File Connection Manager](connection-manager/file-connection-manager.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[接続マネージャー名]**  
 ワークフローにおけるフラット ファイル接続マネージャーの一意な名前を指定します。 指定された名前は、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **[説明]**  
 接続マネージャーの説明を記述します。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、接続マネージャーの目的について記述することをお勧めします。  
  
 **[各列のプロパティを構成します。]**  
 左側のペインで列を選択すると、そのプロパティが右側のペインに表示されます。 データ型プロパティの説明については、次の表を参照してください。 いくつかのプロパティは、一部のフラット ファイル形式でのみ設定できます。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|**[列の型]**|列が区切り形式、固定幅形式、幅合わせしない形式のうちどれであるかを示します。 このプロパティは読み取り専用です。 幅合わせしない形式のファイルとは、最後の列を除くすべての列が固定幅のファイルです。 最後の列は、行区切り記号で区切られます。|  
|**[出力列の幅]**|格納する値をバイト数で指定します。Unicode ファイルの場合、この値は文字数に対応します。 データ フロー タスクでは、この値を使用してフラット ファイル ソースの出力列の幅を設定します。<br /><br /> 注:オブジェクト モデルでは、このプロパティの名前は MaximumWidth です。|  
|**DataType**|使用できるデータ型を一覧から選択します。 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。|  
|**[テキスト修飾子]**|テキスト データが引用符などのテキスト修飾子文字で囲まれているかどうかを示します。 有効な値は、<br /><br /> **True**:フラット ファイルのテキスト データは修飾されます。<br /><br /> **False**:フラット ファイルのテキスト データは修飾されません。|  
|**名前**|わかりやすい列名を指定します。 名前を入力しないと、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によって、列 1、列 2 などの形式で自動的に名前が作成されます。|  
|**[データ スケール]**|数値データの小数点以下の精度を指定します。 これは小数点以下の桁数を表します。 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。|  
|**[列区切り記号]**|使用できる列区切り記号の一覧から、列区切り記号を選択します。 テキストに出現しないと思われる区切り記号を選択してください。 固定幅列の場合、この値は無視されます。<br /><br /> **{CR}{LF}** 。 列は、復帰と改行の組み合わせで区切られます。<br /><br /> **{CR}** 。 列は、復帰で区切られます。<br /><br /> **{LF}** 。 列は、改行で区切られます。<br /><br /> **セミコロン {;}** 。 列は、セミコロンで区切られます。<br /><br /> **コロン {:}** 。 列は、コロンで区切られます。<br /><br /> **コンマ {,}** 。 列は、コンマで区切られます。<br /><br /> **タブ {t}** 。 列は、タブで区切られます。<br /><br /> **縦棒 {&#124;}** 。 列は、縦棒で区切られます。|  
|**[データ精度]**|数値データの精度を指定します。 精度とは、桁数です。 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。|  
|**[入力列の幅]**|格納する値をバイト数で指定します。Unicode ファイルの場合、これは文字数として表示されます。 区切られた列の場合、この値は無視されます。<br /><br /> **注** オブジェクト モデルでは、このプロパティの名前は ColumnWidth です。|  
  
 **[新規作成]**  
 **[新規作成]** をクリックして新しい列を追加します。 既定では、 **[新規作成]** ボタンをクリックすると、新しい列がリストの末尾に追加されます。 さらにこのボタンのドロップダウン リストには、次のオプションがあります。  
  
|値|説明|  
|-----------|-----------------|  
|**[列の追加]**|新しい列をリストの末尾に追加します。|  
|**[前に挿入]**|選択した列の前に新しい列を追加します。|  
|**[後に挿入]**|選択した列の後に新しい列を追加します。|  
  
 **削除**  
 列を選択して **[削除]** をクリックすると、列が削除されます。  
  
 **[型の推測]**  
 **[列の型の推測]** ダイアログ ボックスを使用して、ファイルのサンプル データを評価し、各列のデータ型と長さの推測を取得します。 詳細については、「 [[列の型の推測] ダイアログ ボックスの UI リファレンス](connection-manager/suggest-column-types-dialog-box-ui-reference.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[フラット ファイル接続マネージャー エディター] &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)   
 [[フラット ファイル接続マネージャー エディター] &#40;[列] ページ&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)   
 [[フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  
