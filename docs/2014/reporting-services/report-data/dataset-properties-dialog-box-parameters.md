---
title: '[パラメーター] ([データセットのプロパティ] ダイアログ ボックス) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10150"
- sql12.rtp.rptdesigner.datasetproperties.parameters.f1
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d621895212e72479090363a980ddc00fa2b5a0c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107332"
---
# <a name="dataset-properties-dialog-box-parameters"></a>[パラメーター] ([データセットのプロパティ] ダイアログ ボックス)
  **[データセットのプロパティ]** ダイアログ ボックスの **[パラメーター]** を選択すると、クエリ パラメーター (レポート パラメーターにリンクするクエリ パラメーターを含む) の追加、変更、および削除を実行できます。  
  
 [クエリ] タブでクエリが変更されるたびに、クエリ コマンドが解析されます。 識別されたクエリ パラメーターごとに、大文字と小文字の区別も含めて同じ名前のレポート パラメーターが作成されます。 既定では、クエリ パラメーターは自動的にクエリ パラメーターの一覧に追加され、対応するレポート パラメーターにリンクされます。  
  
 レポート パラメーターの既定値が、クエリ パラメーターにリンクする別のレポート パラメーターに依存している場合は、( **[レポート パラメーターのプロパティ]** ダイアログ ボックスに表示されている) レポート パラメーターの順序が重要になります。 一覧で後方にあるレポート パラメーターは、一覧で前方にあるレポート パラメーターを参照できます。 レポート パラメーターの詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
## <a name="options"></a>および  
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
  
## <a name="see-also"></a>関連項目  
 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-datasets-ssrs.md)   
 [レポート パラメーターの順序の変更 (レポート ビルダーおよび SSRS)](../report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
