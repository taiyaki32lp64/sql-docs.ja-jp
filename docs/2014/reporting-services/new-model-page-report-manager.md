---
title: 新しいモデル ページ (レポート マネージャー) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 27d5bf66-b0e7-489e-a830-ffe2ec8e5350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5b9fdcac2499cdf33d98ba636596218c14704f9d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108208"
---
# <a name="new-model-page-report-manager"></a>[新しいモデル] ページ (レポート マネージャー)
  このページでは、共有データ ソースから既定のレポート モデルを生成できます。 レポート モデルを生成できるのは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多次元データ ソース、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] リレーショナル データ ソース、および Oracle リレーショナル データ ソースだけです。  
  
 レポート マネージャーで生成されるモデルは、共有データ ソースのスキーマに基づいています。 データ ソース内のすべてのテーブルと列に対して、エンティティ、フォルダー、およびフィールドが作成されます。 アイテムを除外したり、モデルの生成方法を決定するオプションを設定することはできません。 モデルをカスタマイズまたは調整する場合は、モデル デザイナーを使用する必要があります。  
  
## <a name="navigation"></a>ナビゲーション  
 ユーザー インターフェイス (UI) のこの場所に移動するには、次の手順に従います。  
  
###### <a name="to-open-the-new-model-page"></a>[新しいモデル] ページを開くには  
  
1.  レポート マネージャーを開き、モデルの生成元の共有データ ソースを探します。  
  
2.  データ ソースの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューで次のいずれかの操作を行います。  
  
    -   **[レポート モデルの生成]** をクリックし、[新しいモデル] ページを開きます。  
  
    -   **[管理]** をクリックし、レポートの [全般] プロパティ ページを開きます。 次に、 **[モデルの生成]** をクリックし、[新しいモデル] ページを開きます。  
  
## <a name="options"></a>および  
 **名前**  
 モデルの名前を指定します。 名前には、少なくとも 1 つの英数字が含まれている必要があります。 また、スペースおよびいくつかの記号を含めることもできます。 名前を指定するときに使用できない記号は次のとおりです。  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **[説明]**  
 モデルの説明を表示します。 レポート マネージャーを使用してこのアイテムを表示すると、フォルダー階層を参照しているときにこの説明が表示されます。  
  
 **場所の変更**  
 新しいモデルのフォルダーの場所を表示します。 **[場所の変更]** ボタンをクリックすると、別の場所を選択できます。  
  
  
