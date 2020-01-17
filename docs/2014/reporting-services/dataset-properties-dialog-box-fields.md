---
title: データセットのプロパティ] ダイアログ ボックスの [フィールド |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasetproperties.fields.f1
- "10140"
ms.assetid: e1367556-736e-4a6b-b9e7-10432a3e50b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 133d905958f0613d9b7ecf2d28c439c15a59eedb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109403"
---
# <a name="dataset-properties-dialog-box-fields"></a>[フィールド] ([データセットのプロパティ] ダイアログ ボックス)
  **[データセットのプロパティ]** ダイアログ ボックスの **[フィールド]** を選択すると、レポート データセットのフィールド コレクションを変更できます。 フィールドの一覧は自動的に作成されますが、 **[フィールド]** を使用してクエリ フィールドや計算フィールドを追加、編集、および削除することができます。  
  
## <a name="options"></a>および  
 **[追加]**  
 新しいクエリ フィールドまたは計算フィールドをデータセットに追加します。  
  
 **削除**  
 選択したフィールドをデータセットから削除します。  
  
 **フィールド名**  
 フィールドの名前を入力します。 フィールドはデータセット内で一意である必要があります。 データセット クエリ内にある既存の各フィールドの名前は、あらかじめ設定されています。  
  
 **[フィールド ソース]**  
 フィールドの値を入力します。  
  
 計算フィールドの場合、フィールド ソースは、データセット クエリで取得した既存のフィールドの名前か、ユーザーが作成した式である必要があります。 たとえば、Sales クエリ フィールドの値の 10 倍を表すフィールドを作成する場合は、 `=10 * Fields!Sales.Value`という式を使用します。  
  
 クエリ フィールドの場合、フィールド ソースは、データセット クエリで取得した既存のフィールドの名前である必要があります。  
  
 **式 ([fx])**  
 計算フィールドを表す式を追加または変更します。 このボタンは、 **[追加]** をクリックして **[計算フィールド]** を選択した場合にのみ表示されます。  
  
## <a name="see-also"></a>参照  
 [データセット フィールド コレクション &#40;レポート ビルダーおよび SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
