---
title: '[パラメーター] ([データセットのプロパティ] ダイアログ ボックス) | Microsoft Docs'
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: reference
f1_keywords:
- "10150"
- sql13.rtp.rptdesigner.datasetproperties.parameters.f1
- "10023"
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 66e0d56cbff57a6100ab8c61436ba6bcddf15382
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573175"
---
# <a name="dataset-properties-dialog-box-parameters"></a>[パラメーター] ([データセットのプロパティ] ダイアログ ボックス)
  **[データセットのプロパティ]** ダイアログ ボックスの **[パラメーター]** を選択すると、クエリ パラメーター (レポート パラメーターにリンクするクエリ パラメーターを含む) の追加、変更、および削除を実行できます。  
  
 [クエリ] タブでクエリが変更されるたびに、クエリ コマンドが解析されます。 識別されたクエリ パラメーターごとに、大文字と小文字の区別も含めて同じ名前のレポート パラメーターが作成されます。 既定では、クエリ パラメーターは自動的にクエリ パラメーターの一覧に追加され、対応するレポート パラメーターにリンクされます。  
  
 レポート パラメーターの既定値が、クエリ パラメーターにリンクする別のレポート パラメーターに依存している場合は、( **[レポート パラメーターのプロパティ]** ダイアログ ボックスに表示されている) レポート パラメーターの順序が重要になります。 一覧で後方にあるレポート パラメーターは、一覧で前方にあるレポート パラメーターを参照できます。 レポート パラメーターの詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **[追加]**  
 一覧に新しいパラメーターを追加します。  
  
 **削除**  
 選択したパラメーターを一覧から削除します。  
  
 **[パラメーター名]**  
 **[データセットのプロパティ]** ダイアログ ボックスの **[クエリ]** タブでデータセットに追加したクエリ パラメーターの名前を入力します。  
  
 **[パラメーター値]**  
 クエリ パラメーターの値を入力します。 この値には、静的な値、またはレポート内のオブジェクトを参照するがレポート アイテムやフィールドは参照できない式を指定できます。 既定では、 **[値]** に、レポート パラメーターを参照する式が設定されています。  
  
 **上矢印**  
 選択したパラメーターを一覧内で上に移動します。  
  
 **下矢印**  
 選択したパラメーターを一覧内で下に移動します。  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [レポート パラメーターの順序の変更 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
