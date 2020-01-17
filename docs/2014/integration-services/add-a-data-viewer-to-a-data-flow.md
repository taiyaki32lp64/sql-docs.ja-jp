---
title: データ フローにデータ ビューアーの追加 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data viewers [Integration Services]
- data flow [Integration Services], data viewers
- adding data viewers
ms.assetid: 5e573274-a170-4132-bfc8-a8ff3a8411e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cbd45caac75d4fac3b5fffc305a9f359193191a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062092"
---
# <a name="add-a-data-viewer-to-a-data-flow"></a>データ フローにデータ ビューアーを追加する
  このトピックでは、データ フローにデータ ビューアーを追加して構成する方法について説明します。 データ ビューアーには、2 つのデータ フロー コンポーネント間を移動するデータが表示されます。 たとえば、データ ビューアーでは、データ ソースから抽出されたデータを、データ フローの変換で変更される前の状態で表示できます。  
  
 パスは、データ フロー コンポーネントの出力を別のコンポーネントの入力に連結することにより、データ フロー内のコンポーネントを連結します。  
  
 データ ビューアーをパッケージに追加するには、パッケージにデータ フロー タスクが含まれていて、少なくとも 2 つのデータ フロー コンポーネントが接続されている必要があります。  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>データ フローにデータ ビューアーを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  アクティブになっていない場合は、 **[制御フロー]** タブをクリックします。  
  
4.  データ ビューアーをアタッチするデータ フローに対応するデータ フロー タスクをクリックし、 **[データ フロー]** タブをクリックします。  
  
5.  2 つのデータ フロー コンポーネント間のパスを右クリックし、 **[編集]** をクリックします。  
  
6.  **[全般]** ページで、パスのプロパティを表示および編集できます。 たとえば、 **[PathAnnotation]** ボックスの一覧で、パスの横に表示される注釈を選択できます。  
  
7.  **[メタデータ]** ページで、列のメタデータを表示し、メタデータをクリップボードにコピーできます。  
  
8.  **[データ ビューアー]** ページで、 **[データ ビューアーを有効にする]** をクリックします。  
  
9. [表示する列] 領域で、データ ビューアーに表示する列を選択します。 既定では、表示可能なすべての列が選択され、 **[表示する列]** の一覧に表示されます。 表示しない列は、選択してから左矢印をクリックして、 **[未使用の列]** の一覧に移動させます。  
  
    > [!NOTE]  
    >  グリッドでは、DT_DATE、DT_DBTIME2、DT_FILETIME、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、および DT_DBTIMESTAMPOFFSET の各データ型を表す値は、ISO 8601 に従って書式設定された文字列として表示され、`T` 区切りが空白区切りに置き換わります。 DT_DATE データ型および DT_FILETIME データ型を表す値には、秒の小数部を表す 7 桁が含まれています。 DT_FILETIME データ型では秒の小数部が 3 桁のみ格納されるため、残りの 4 桁についてはグリッドに 0 が表示されます。 DT_DBTIMESTAMP データ型を表す値には、秒の小数部を表す 3 桁が含まれています。 DT_DBTIME2、DT_DBTIMESTAMP2、および DT_DBTIMESTAMPOFFSET の各データ型を表す値については、秒を表す小数点以下桁数が、列のデータ型で指定された小数点以下桁数と一致します。 ISO 8601 形式の詳細については、「 [日付および時刻の形式](../../2014/integration-services/date-and-time-formats.md)」を参照してください。 データ型の詳細については、「 [Integration Services のデータ型](data-flow/integration-services-data-types.md)」を参照してください。  
  
10. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services の変換](data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](data-flow/integration-services-paths.md)   
 [[データ フロー]](data-flow/data-flow.md)   
 [データ フローのデバッグ](troubleshooting/debugging-data-flow.md)  
  
  
