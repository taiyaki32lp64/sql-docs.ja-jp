---
title: Transact-SQL デバッガー
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, introduction
ms.assetid: 6e914699-0d85-46c2-aa2d-3e339ac2c4ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d82ab18ebf1a8b7771e6afd37dcd14ed58ed35c8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243019"
---
# <a name="transact-sql-debugger"></a>Transact-SQL デバッガー
  
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーを使用すると、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コードの実行時の動作を確認してエラーを検出できます。 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウをデバッグ モードに設定した後、特定のコード行で実行を一時停止し、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで使用されている (またはステートメントから返される) 情報やデータを調べることができます。  
  
## <a name="stepping-through-transact-sql-code"></a>Transact-SQL コードのステップ実行  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディター ウィンドウがデバッグ モードのときに [!INCLUDE[ssDE](../../includes/ssde-md.md)] コードに対して次の操作を行うことができます。  
  
-   個々の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントにブレークポイントを設定する。  
  
     実行を一時的に停止してデータを調査するには、その位置をブレークポイントで指定します。 デバッガーを起動すると、デバッガーはクエリ エディター ウィンドウ内の最初のコード行で一時停止します。 設定した最初のブレークポイントまで実行するには、 **続行** 機能を使用します。 
  **続行** 機能は、現在一時停止しているウィンドウの場所から次のブレークポイントまで実行するためにも使用できます。 ブレークポイントは編集することができます。実行を一時停止する条件や、 **[出力]** ウィンドウに表示する情報など、その動作を指定できるほか、ブレークポイントの場所を変更することもできます。  
  
-   次のステートメントにステップ インする。  
  
     ステートメントのセット内を 1 つずつ移動して、その動作を確認できます。  
  
-   ストアド プロシージャまたは関数の呼び出しにステップ インまたはステップ オーバーする。  
  
     ストアド プロシージャにエラーがないことがわかっている場合は、ストアド プロシージャにステップ オーバーできます。 プロシージャは完全に実行され、その結果がコードに返されます。  
  
     ストアド プロシージャまたは関数をデバッグする場合、モジュールにステップ インできます。 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] に、モジュールのソース コードが表示された新しい [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが開かれた後、ウィンドウがデバッグ モードに切り替えられ、モジュールの最初のステートメントで実行が一時停止します。 その後、モジュールのコードに対して、ブレークポイントの設定やコードのステップ実行などの操作を行うことができます。  
  
 デバッガーでのコードの操作については、「 [Transact-SQL コードのステップ実行](step-through-transact-sql-code.md)」を参照してください。  
  
## <a name="viewing-debugger-information"></a>デバッガー情報の表示  
 デバッガーが特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで実行を一時停止するたびに、次のデバッガー ウィンドウを使用して現在の実行状態を表示できます。  
  
-   [**ローカル**] と [**ウォッチ]。** これらのウィンドウには、現在割り当てられている [!INCLUDE[tsql](../../includes/tsql-md.md)] 式が表示されます。 式は、単一のスカラー式に評価される [!INCLUDE[tsql](../../includes/tsql-md.md)] 句です。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] 変数、パラメーター、または、組み込み関数を参照する、名前が @@ で始まる表示式がサポートされます。 また、これらのウィンドウには、式に現在割り当てられているデータ値も表示されます。  
  
-   **[クイックウォッチ.** このウィンドウには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 式の値が表示されます。式を **[ウォッチ]** ウィンドウに保存することができます。  
  
-   **区切り.** このウィンドウには、現在設定されているブレークポイントが表示されます。ブレークポイントを管理できます。  
  
-   **呼び出し履歴。** このウィンドウには、現在の実行場所が表示されます。 また、実行が元のクエリ エディター ウィンドウから関数、ストアド プロシージャ、またはトリガー経由で現在の実行場所までどのように渡されたかについての情報も表示されます。  
  
-   **Output.** このウィンドウには、各種のメッセージやプログラム データ (たとえばデバッガーからのシステム メッセージ) が表示されます。  
  
-   **結果**と**メッセージ。** クエリ エディター ウィンドウ上のこれらのタブには、前に実行された [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの結果が表示されます。  
  
## <a name="transact-sql-debugger-tasks"></a>Transact-SQL デバッガーのタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|リモート デバッグに必要な構成を [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーに対して行う方法について説明します。|[Transact-sql デバッガーの構成](configure-firewall-rules-before-running-the-tsql-debugger.md)|  
|デバッガーの操作を開始、停止、および制御する方法について説明します。|[Transact-sql デバッガーの実行](transact-sql-debugger.md)|  
|
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーを使用してコードをステップ実行する方法について説明します。|[Transact-sql コードのステップ実行](step-through-transact-sql-code.md)|  
|デバッガーを使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] データ (パラメーター、変数など) およびシステム情報を表示する方法について説明します。|[Transact-sql デバッガー情報](transact-sql-debugger-information.md)|  
  
## <a name="see-also"></a>参照  
 [クエリエディターとテキストエディター &#40;SQL Server Management Studio&#41;](../scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
