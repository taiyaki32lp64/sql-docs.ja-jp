---
title: '[クイック ウォッチ] ダイアログ ボックス'
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d41aab8066b4ce1ee4e45fa9c363e60479868a5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243038"
---
# <a name="quickwatch-dialog-box"></a>[クイック ウォッチ] ダイアログ ボックス
  [**クイックウォッチ**] ダイアログボックスを使用すると、コードをデバッグ[!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]するときに、変数やパラメーターなど、1つの式のデータ型と値をすばやく表示できます。 複数の式を確認するために、 **[ウォッチ]** ウィンドウに式を追加することもできます。  
  
## <a name="task-list"></a>タスク一覧  
 **[クイックウォッチ] ダイアログボックスにアクセスするには**  
  
-   
  **[デバッグ]** メニューの **[クイック ウォッチ]** をクリックします。  
  
 **式に関する情報を表示するには**  
  
1.  
  **[式]** ボックスで、目的の式を入力または選択します。 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] 式がサポートされています。  
  
    -   変数。  
  
    -   パラメーター。  
  
    -   名前が @@ で始まるシステム関数。  
  
    -   1 つまたは複数の変数、パラメーター、またはシステム関数に演算子を適用して作成された式 (@IntegerCounter + 1、FirstName + LastName など)。  
  
    -   単一の値を返す Transact-SQL ステートメント (SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1 など)。  
  
2.  
  **[再評価]** をクリックします。  
  
 **ウォッチウィンドウにクイックウォッチ式を追加するには**  
  
-   
  **[ウォッチ式の追加]** をクリックします。  
  
 **[クイックウォッチ] 式の値を変更するには**  
  
-   式を右クリックし、 **[値の編集]** を選択します。  
  
## <a name="options"></a>オプション  
 **式の一覧**  
 現在選択されている式を表示します。 このドロップダウン リストには、選択して表示できる式のセットが含まれています。 一覧の式は、 **[呼び出し履歴]** ウィンドウで現在選択されているスタック フレームのスコープで使用できる式です。 別の式を表示するには、式を入力するか、一覧から式を選択します。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは、変数、パラメーター、および名前が @@ で始まるシステム関数の式がサポートされます。  
  
 **値グリッド**  
 現在監視されている式のプロパティを表示します。  
  
 **指定**  
 監視対象の [!INCLUDE[tsql](../../includes/tsql-md.md)] 式です。  
  
 **値**  
 式に現在割り当てられている値を表示します。 式に現在値がない場合は、空白になります。  
  
 式の長さが **[値]** 列の幅よりも長い場合は、その式の **[値]** セルにポインターを移動するとツールヒントに完全な値が表示されます。  
  
 
  **[値]** セルの虫眼鏡アイコンは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガー ビジュアライザーが使用可能であることを示します。 一覧では、 **[テキスト ビジュアライザー]**、 **[XML ビジュアライザー]**、または **[HTML ビジュアライザー]** を指定できます。 デバッガー ビジュアライザーを開始するには、虫眼鏡アイコンをクリックします。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーによりダイアログ ボックスが開き、データがそのデータ型に適した形式で表示されます。  
  
 **各種**  
 式のデータ型を表示します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql デバッガー](transact-sql-debugger.md)   
 [Transact-sql デバッガー情報](transact-sql-debugger-information.md)   
 [ウォッチウィンドウ](transact-sql-debugger-watch-window.md)   
 [[ローカル] ウィンドウ](transact-sql-debugger-locals-window.md)   
 [呼び出し履歴ウィンドウ](transact-sql-debugger-call-stack-window.md)   
 [式 &#40;Transact-sql&#41;](/sql/t-sql/language-elements/expressions-transact-sql)  
  
  
