---
title: ローカル ウィンドウ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cac6d8c5a231d51f89661baf57bec2fd0d9471fd
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68253520"
---
# <a name="transact-sql-debugger---locals-window"></a>Transact-SQL デバッガー - [ローカル] ウィンドウ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **[ローカル]** ウィンドウには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーの現在のスコープ内にあるローカル式についての情報が表示されます。 スコープは、 **[呼び出し履歴]** ウィンドウで選択された現在の呼び出し履歴フレームに設定されます。 ローカル式を表示するには、デバッグ モードである必要があります。  
  
## <a name="task-list"></a>タスク一覧  
 **[ローカル] ウィンドウにアクセスするには**  
  
-   **[デバッグ]** メニューの **[ウィンドウ]** をポイントし、 **[ローカル]** をクリックします。  
  
 **式の値を変更するには**  
  
-   式を右クリックし、 **[値の編集]** を選択します。  
  
## <a name="columns"></a>[列]  
 **[名前]**  
 ローカル式の名前です。 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは、変数、パラメーター、および名前が @@ で始まるシステム関数が一覧表示されます。  
  
 **Value**  
 ローカル式に現在割り当てられている値を表示します。 式に値が割り当てられていない場合、この列は空白です。  
  
 式の長さが **[値]** 列の幅よりも長い場合は、その式の **[値]** セルにポインターを移動するとツールヒントに完全な値が表示されます。  
  
 **[値]** セルの虫眼鏡アイコンは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガー ビジュアライザーが使用可能であることを示します。 一覧では、 **[テキスト ビジュアライザー]** 、 **[XML ビジュアライザー]** 、または **[HTML ビジュアライザー]** を指定できます。 デバッガー ビジュアライザーを開始するには、虫眼鏡アイコンをクリックします。 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーによりダイアログ ボックスが開き、データがそのデータ型に適した形式で表示されます。  
  
 **型**  
 式のデータ型を表示します。  
  
## <a name="see-also"></a>参照  
 [Transact-SQL デバッガー](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL デバッガー情報](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [[ウォッチ] ウィンドウ](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [[呼び出し履歴] ウィンドウ](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [[クイック ウォッチ] ダイアログ ボックス](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
