---
title: '[コマンド] ウィンドウ'
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26306f8ad2adf01ebdcbf1b52169f1c2ec964920
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243080"
---
# <a name="command-window"></a>[コマンド] ウィンドウ
  [コマンド **] ウィンドウ**を使用すると、現在デバッグ中の[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]クエリエディターウィンドウのコードに対して、デバッグコマンドや編集コマンドなどのコマンドを実行できます。 
  **[コマンド]** ウィンドウを使用するには、デバッグ モードである必要があります。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **[コマンド]** ウィンドウでもサポートされているコマンドの多くをサポートしています。 詳細については、 [Visual Studio のコマンド ウィンドウに関するページ](https://go.microsoft.com/fwlink/?LinkId=112007)を参照してください。  
  
## <a name="task-list"></a>タスク一覧  
 **[コマンド] ウィンドウにアクセスするには**  
  
-   
  **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
 **変数の値を出力するには**  
  
-   
  **[コマンド] ウィンドウ**で、「**Debug.Print \<変数名>**」と入力し、Enter キーを押します。  
  
 **現在のスレッドに関する情報を一覧表示するには**  
  
-   **コマンドウィンドウ**で、「」 `Debug.ListThread`と入力し、enter キーを押します。  
  
 **[クイックウォッチ] ウィンドウに変数を追加するには**  
  
-   
  **[コマンド] ウィンドウ**で、「**Debug.QuickWatch \<変数名>**」と入力し、Enter キーを押します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql デバッガー](transact-sql-debugger.md)  
