---
title: テーブル値オブジェクト (列) のプロパティ (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.designers.properties.QueryViewColumn
ms.assetid: 212d9bcd-aded-4313-a6b9-d7e2270e5954
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14c2fff96c89ee696df1a437f958e4560bfab142
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204530"
---
# <a name="table-valued-object-column-properties-visual-database-tools"></a>テーブル値オブジェクト (列) のプロパティ (Visual Database Tools)
  クエリ デザイナーとビュー デザイナーの **[ダイアグラム]** ペインでテーブル値オブジェクト内の列を選択したときに、このプロパティが表示されます。  
  
> [!NOTE]  
>  このトピックでは、プロパティを五十音順ではなくカテゴリ別に示しています。  
  
> [!NOTE]  
>  使用中の設定やエディションに応じて、表示されるダイアログ ボックスとメニュー コマンドがヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** を選択してください。  
  
 **[IDENTITY] カテゴリ**  
 展開すると、 **[名前]** プロパティが表示されます。  
  
 **名前**  
 選択した列の名前が表示されます。  
  
 **クエリ デザイナー カテゴリ**  
 展開すると、 **[NULL を許容]** 、 **[照合順序]** 、 **[長さ]** 、 **[データ型]** 、 **[精度]** 、 **[スケール]** 、 **[サイズ]** のプロパティが表示されます。  
  
 **[NULL を許容]**  
 列のデータ型で NULL が許容されるかどうかが表示されます。  
  
 **照合順序**  
 選択した列における照合順序の設定が表示されます。 照合順序は、Table Designer の [列のプロパティ] タブで設定できます。  
  
 **データ型**  
 選択した列のデータ型が表示されます。  
  
 **[データ型]**  
 選択した列のデータ型で許容される文字または数字の数が表示されます。 このプロパティは、文字に基づくデータ型にのみ使用できます。  
  
> [!NOTE]  
>  バイト単位の大きさについては、以降に示す **[サイズ]** プロパティの説明を参照してください。  
  
 **[精度]**  
 数値データ型で許容される最大桁数が表示されます。 数値データ型でないデータ型の場合、このプロパティには **0** と表示されます。  
  
 **[スケール]**  
 数値データ型の小数点の右側にある桁数の最大数が表示されます。 この値は、有効桁数以下である必要があります。 数値データ型でないデータ型の場合、このプロパティには **0** と表示されます。  
  
 **[サイズ]**  
 列のデータ型で許容されるサイズがバイト単位で表示されます。 たとえば、nchar データ型の長さが 10 (文字数) でも、Unicode 文字セットの場合のサイズは 20 になります。  
  
  
