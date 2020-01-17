---
title: '[ブレークポイント] ウィンドウ | Microsoft Docs'
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 11/04/2019
helpviewer_keywords:
- Breakpoints Window [Transact-SQL]
ms.assetid: bad88d10-fdd5-4d3d-b5ea-a4f063847485
monikerRange: '>= sql-server-2014 || = sqlallproducts-allversions'
ms.openlocfilehash: cc5600a7cd9e933046700204a8dac916199832c6
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73638010"
---
# <a name="transact-sql-debugger---breakpoints-window"></a>Transact-SQL デバッガー - [ブレークポイント] ウィンドウ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**[ブレークポイント]** ウィンドウには、現在の [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターで設定されているすべてのブレークポイントが表示されます。 ブレークポイントを管理するには、 **[ブレークポイント]** ウィンドウのツール バーを使用します。 ブレークポイントとは、デバッグ モードでコードの実行を一時停止する箇所で、デバッグ データを表示できます。

## <a name="task-list"></a>タスク一覧

**[ブレークポイント] ウィンドウにアクセスするには**

- **[デバッグ]** メニューで **[ウィンドウ]** を選択し、 **[ブレークポイント]** を選択します。

## <a name="breakpoints-window-columns"></a>[ブレークポイント] ウィンドウの列

既定では、 **[ブレークポイント]** ウィンドウには次の列が表示されます。  

**[名前]**  
ブレークポイントの名前が表示されます。 ブレークポイント名はデバッガーによって指定されます。 この名前には、そのブレークポイントを含むデータベース エンジンのクエリ エディター ウィンドウの名前、およびそのブレークポイントが設定されているクエリ エディター内の行番号が含まれます。  

**条件**  
**[(条件なし)]** が表示されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーは、ブレークポイント条件の設定をサポートしていません。

**[ヒット カウント]**  
**[常に中断]** が表示されます。

**[列]** ボックスの一覧で次の列を選択して、それらの列を追加したり、削除したりできます。  

**Assert**  
**[(なし)]** が表示されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーは、ブレークポイント フィルターの設定をサポートしていません。

**[ヒット時]**  
**[中断]** が表示されます。

**言語**  
**を表す** [Transact-SQL] [!INCLUDE[tsql](../../includes/tsql-md.md)]が表示されます。  

**関数**  
ブレークポイントが設定されている行番号が表示されます。  

**[最近使ったファイル]**  
ブレークポイントを含むソース ファイルの名前、およびブレークポイントが設定されている行番号が表示されます。

**Address**  
[!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーはこの機能をサポートしていません。  

**[処理]**  
**プロセスであることを示す** [SQL] [!INCLUDE[ssDE](../../includes/ssde-md.md)] が表示されます。 この後に、コードが実行される [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスの名前が表示されます。

## <a name="breakpoints-window-toolbar"></a>[ブレークポイント] ウィンドウのツール バー

現在の [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディター ウィンドウにアクティブなブレークポイントがある場合、それらのブレークポイントの管理に使用できるツール バーが **[ブレークポイント]** ウィンドウに表示されます。

**削除**  
選択したブレークポイントを削除します。

**[すべてのブレークポイントの削除]**  
**[ブレークポイント]** ウィンドウに表示されているすべてのブレークポイントを削除します。  

**[すべてのブレークポイントを無効にする]**  
すべてのブレークポイントを無効にして、コードの実行が停止されなくなるようにします。ただし、ブレークポイントは削除されません。 すべてのブレークポイントを無効にすると、このボタンは **[すべてのブレークポイントを有効にする]** になります。

**[すべてのブレークポイントを有効にする]**  
すべてのブレークポイントを有効にして、コードの実行が停止されるようにします。 すべてのブレークポイントを有効にすると、このボタンは **[すべてのブレークポイントを無効にする]** になります。  

**[ソース コードへ移動]**  
選択したブレークポイントを含むクエリ エディター内の行にカーソルを移動します。

**[列]**  
**[ブレークポイント]** ウィンドウで表示できるすべての列が表示されます。 チェック ボックスによって、表示される列を指定します。 **[ブレークポイント]** ウィンドウの列を追加または削除するには、一覧でその列を選択します。

## <a name="see-also"></a>参照

[Transact-SQL デバッガー](../../relational-databases/scripting/transact-sql-debugger.md)
