---
title: 複合ドメインへの列のマップ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9422412-8a3d-45ae-af7f-072c902a09ba
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9ce189688bd33f3cb63280e4fa44bb2284ee9e8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900038"
---
# <a name="map-columns-to-composite-domains"></a>複合ドメインへの列のマップ
  複合ドメインは 2 つ以上の単一ドメインで構成されています。 ドメインに複数の列をマップすることも、区切られた値を含む単一の列をドメインにマップすることもできます。  
  
 複数の列がある場合は、複合ドメインの各単一ドメインに列をマップして、データ クレンジングに複合ドメイン ルールを適用する必要があります。 Data Quality Client の複合ドメインに含まれる単一ドメインを選択します。 詳細については、「 [複合ドメインの作成](../../../data-quality-services/create-a-composite-domain.md)」をご覧ください。  
  
 区切られた値を含む単一の列がある場合は、その単一の列を複合ドメインにマップする必要があります。 値は、単一ドメインが複合ドメインに表示されるのと同じ順序で表示される必要があります。 データ ソースの区切り記号は、複合ドメインの値の解析に使用される区切り記号と一致する必要があります。 複合ドメインの区切り記号を選択し、Data Quality Client で他のプロパティを設定します。 詳細については、「 [複合ドメインの作成](../../../data-quality-services/create-a-composite-domain.md)」をご覧ください。  
  
### <a name="to-map-multiple-columns-to-a-composite-domain"></a>複数の列を複合ドメインにマップするには  
  
1.  DQS クレンジング変換を右クリックして、 **[編集]** をクリックします。  
  
2.  **[接続マネージャー]** タブで、複合ドメインが使用可能なドメインの一覧に表示されていることを確認します。  
  
3.  **[マッピング]** タブの **[使用できる入力列]** 領域で列を選択します。  
  
4.  **[入力列]** フィールドにリストされている列ごとに、 **[ドメイン]** フィールドで単一ドメインを選択します。 複合ドメイン内の単一ドメインのみ選択します。  
  
5.  必要に応じて、 **[ソースの別名]** 、 **[出力の別名]** 、および **[状態の別名]** の各フィールドに表示される名前を変更します。  
  
6.  必要に応じて、 **[詳細設定]** タブでプロパティを設定します。プロパティの詳細については、「 [[DQS クレンジング変換エディター] ダイアログ ボックス](../../dqs-cleansing-transformation-editor-dialog-box.md)」をご覧ください。  
  
### <a name="to-map-a-column-with-delimited-values-to-a-composite-domain"></a>区切られた値を含む列を複合ドメインにマップするには  
  
1.  DQS クレンジング変換を右クリックして、 **[編集]** をクリックします。  
  
2.  **[接続マネージャー]** タブで、複合ドメインが使用可能なドメインの一覧に表示されていることを確認します。  
  
3.  **[マッピング]** タブの **[使用できる入力列]** 領域で列を選択します。  
  
4.  **[入力列]** フィールドに表示されている列に対して、 **[ドメイン]** フィールドで複合ドメインを選択します。  
  
5.  必要に応じて、 **[ソースの別名]** 、 **[出力の別名]** 、および **[状態の別名]** の各フィールドに表示される名前を変更します。  
  
6.  必要に応じて、 **[詳細設定]** タブでプロパティを設定します。プロパティの詳細については、「 [[DQS クレンジング変換エディター] ダイアログ ボックス](../../dqs-cleansing-transformation-editor-dialog-box.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [DQS クレンジング変換](dqs-cleansing-transformation.md)  
  
  
