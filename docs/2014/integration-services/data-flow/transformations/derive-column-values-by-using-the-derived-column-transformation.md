---
title: 派生列変換を使用して列の値を取得する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- columns [Integration Services]
- derived columns
- columns [Integration Services], values
- Derived Column transformation
ms.assetid: 28b07746-fc6f-42b2-b741-9de6fac3f29c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 39b8e065b6b3cbd013089700de07376edc9a656c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770696"
---
# <a name="derive-column-values-by-using-the-derived-column-transformation"></a>派生列変換を使用して列の値を取得する
  派生列変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つの変換元があらかじめ含まれている必要があります。  
  
 派生列変換では、式を使用して既存の値を更新したり、新しい列に値を追加したりします。 新しい列に値を追加することを選択すると、 **[派生列変換エディター]** ダイアログ ボックスによって式が評価され、それに応じて列のメタデータが定義されます。 たとえば、2 つの列 (ぞれぞれデータ型が DT_WSTR で長さが 50) があり、式がこの 2 つの列の値の間にスペースを 1 つ入れて連結する場合、新しい列はデータ型が DT_WSTR で長さが 101 になります。 新しい列のデータ型は更新することができます。 唯一の要件は、挿入されたデータと互換性があるデータ型であることです。 たとえば、整数データ型の列に日付の値を割り当てると、 **[派生列変換エディター]** ダイアログ ボックスによって検証エラーが生成されます。 選択したデータ型に応じて、列の長さ、有効桁数、小数点以下桁数、およびコード ページを指定することができます。  
  
### <a name="to-derive-column-values"></a>列の値を取得するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、派生列変換をデザイン画面にドラッグします。  
  
4.  派生列変換をデータ フローに連結します。連結するには、変換元または前の変換から派生列変換にコネクタをドラッグします。  
  
5.  派生列変換をダブルクリックします。  
  
6.  **[派生列変換エディター]** ダイアログ ボックスで、変数、列、関数、および演算子を、グリッドの **[式]** 列にドラッグし、条件として使用する式を構築します。 **[式]** 列には、式を直接入力することもできます。  
  
    > [!NOTE]  
    >  式が有効でない場合、式のテキストは強調表示され、列のツールヒントにエラーの説明が表示されます。  
  
7.  **[派生列]** 一覧で、 **[\<新しい列として追加>]** を選択して式の評価結果を新しい列に書き込みます。または、既存の列を選択し、評価結果で更新します。  
  
     新しい列を使用することを選択した場合は、 **[派生列変換エディター]** ダイアログ ボックスによって式が評価され、データ型、長さ、有効桁数、小数点以下桁数、およびコード ページに応じて列にデータ型が割り当てられます。  
  
8.  新しい列を使用する場合は、 **[データ型]** 一覧でデータ型を選択します。 選択したデータ型によっては、必要に応じて **[長さ]** 、 **[有効桁数]** 、 **[小数点以下桁数]** 、および **[コード ページ]** 列の値を更新します。 既存の列のメタデータは変更できません。  
  
9. 必要に応じ、 **[派生列名]** 列の値を変更します。  
  
10. エラー出力を構成するには、 **[エラー出力の構成]** をクリックします。 詳細については、「 [データ フロー コンポーネントでエラー出力を構成する](../../configure-an-error-output-in-a-data-flow-component.md)」を参照してください。  
  
11. **[OK]** をクリックします。  
  
12. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [Derived Column Transformation](derived-column-transformation.md)   
 [Integration Services のデータ型](../integration-services-data-types.md)   
 [Integration Services の変換](integration-services-transformations.md)   
 [Integration Services のパス](../integration-services-paths.md)   
 [[データ フロー タスク]](../../control-flow/data-flow-task.md)   
 [Integration Services (SSIS) 式](../../expressions/integration-services-ssis-expressions.md)  
  
  
