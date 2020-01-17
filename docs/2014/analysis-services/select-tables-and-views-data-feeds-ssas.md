---
title: テーブルとビュー (データ フィード) を選択します (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviewsdf.f1
ms.assetid: 6c4fafe0-e02e-47d1-b8bc-e70e872690af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82fcf08a84a06d33c33a520ce351f6c685092a15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069278"
---
# <a name="select-tables-and-views-data-feeds-ssas"></a>[テーブルとビューの選択] (データ フィード) (SSAS)
  **テーブルのインポート ウィザード** のこのページを使用すると、データのインポート元となるテーブルとビューを選択できます。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]からウィザードにアクセスするには、 **[モデル]** メニューの **[データ ソースからのインポート]** をクリックします。  
  
 このページに表示されるテーブルとビューは、インポートの成功を保証するものではありません。 [権限借用情報] ページで指定されたユーザーに、選択したデータベースの読み取り権限がないと、インポートは失敗します。  
  
 Windows 認証を使用したデータ ソースの場合、[テーブルとビューの選択] ダイアログにおけるテーブルおよびビューは、現在のユーザーの資格情報を使用してフェッチされます。 その他のデータ ソースについては、接続文字列に指定された資格情報を使用してデータがフェッチされます。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **データ フィード URL**  
 選択したデータ フィードの URL が表示されます。  
  
 **テーブルとビュー**  
 データ フィードのテーブルおよびビューが一覧表示されます。 インポートする各テーブルとビューの横にあるチェック ボックスをオンにします。  
  
 **ソース テーブル**  
 データ ソースの種類に応じて、ソース テーブルの名前を指定します。  
  
 **表示名**  
 ソース テーブルの表示名を指定します。 既定では、 **[ソース テーブル]** 列に表示されるソース テーブルの名前が列に表示されます。  
  
 **フィルターの詳細**  
 インポートするデータにフィルターが適用されると、 **[フィルターの詳細]** ダイアログ ボックスにデータ インポート フィルターが表示されます。 詳細については、「[[フィルターの詳細] (SSAS)](filter-details-ssas.md)」を参照してください。  
  
 **プレビューとフィルター**  
 インポートするデータにフィルターを適用するときに使用する **[選択したテーブルのプレビュー]** ダイアログ ボックスが表示されます。 詳細については、「[[選択したテーブルのプレビュー] (SSAS)](preview-selected-table-ssas.md)」を参照してください。  
  
 **関連テーブルを選択します。**  
 選択したテーブルとビューに関連するテーブルを選択します。  
  
  
