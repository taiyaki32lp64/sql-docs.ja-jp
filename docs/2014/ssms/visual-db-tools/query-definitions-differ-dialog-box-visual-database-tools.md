---
title: '[クエリの定義が異なります] ダイアログ ボックス (Visual Database Tools) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69639
- vdtsql.chm:69640
- vdt.dlgbox.querydefinitionsdiffer
ms.assetid: 90383473-2922-40e5-9682-3850849aa856
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 781963ddd2011c9e16cf67fdcd878039527546cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294458"
---
# <a name="query-definitions-differ-dialog-box-visual-database-tools"></a>[クエリの定義が異なります] ダイアログ ボックス (Visual Database Tools)
  このダイアログ ボックスは、クエリがダイアグラム ペインおよび抽出条件ペインでグラフィカルに表示できず、SQL ペインでしか編集できないことを通知します。  
  
 SQL ペインで SQL ステートメントを入力または編集してから、別のペインに移動するか、クエリを検査するか、またはクエリを実行しようとしたときに、次の条件のいずれかが当てはまる場合に表示されます。  
  
-   SQL ステートメントが不完全であるか、構文エラーがある。  
  
-   SQL ステートメントは有効だが、グラフィカル ペインでサポートされていない (Union クエリなど)。  
  
-   SQL ステートメントは有効だが、使用しているデータ接続に固有の構文が含まれている。  
  
> [!TIP]  
>  **[クエリ]** ツール バーの **[SQL 構文の確認]** ボタンを使用すると、ステートメントが有効かどうかを確認できます。  
  
 ダイアログ ボックスには、SQL ステートメントが表示できない理由を示すメッセージが表示され、どのように処理するかの決定が求められます。  
  
> [!NOTE]  
>  ダイアグラム ペインおよび抽出条件ペインが非表示になっている場合、 **[クエリの定義が異なります]** ダイアログ ボックスは表示されません。  
  
## <a name="options"></a>および  
 **[無視] ボタン**  
 SQL ステートメントを受け入れてさらに編集するか実行する場合は、このボタンをクリックします。 ステートメントを受け入れると、ダイアグラム ペインと抽出条件ペインが淡色表示になり、SQL ペインのステートメントを反映しないことが示されます。  
  
 **[元に戻す] ボタン**  
 SQL ペインへの変更を破棄する場合は、このボタンを選択します。  
  
> [!NOTE]  
>  ステートメントが正しいにもかかわらずクエリおよびビュー デザイナーによってグラフィカルにサポートされない場合は、ダイアグラム ペインと抽出条件ペインには表示されませんが、実行することはできます。 たとえば、Union クエリを入力した場合、ステートメントは実行できますが、他のペインには表示されません。  
  
## <a name="see-also"></a>参照  
 [クエリおよびビュー デザイナー ツール (Visual Database Tools)](visual-database-tools.md)  
  
  
