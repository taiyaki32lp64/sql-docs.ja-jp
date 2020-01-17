---
title: Transact-SQL デバッガー情報 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, Locals Window
- Transact-SQL debugger, Watch Window
- Transact-SQL debugger, Threads Window
- Transact-SQL debugger, Call Stack Window
- Transact-SQL debugger, QuickWatch
- Transact-SQL debugger, viewing information
ms.assetid: b99819cc-f388-41a1-b304-36e78ce24147
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6329776bd998a8d90cbadd577132a500020515b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68253553"
---
# <a name="transact-sql-debugger---information"></a>Transact-SQL デバッガー情報
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  デバッガーが特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで実行を一時停止するたびに、さまざまなデバッガー ウィンドウを使用して現在の実行状態を表示できます。  
  
## <a name="debugger-windows"></a>デバッガー ウィンドウ  
 デバッガー モードでは、デバッガーにより、メイン [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ウィンドウの下部に 2 つのウィンドウが開かれます。 デバッガーをこれら 2 つのウィンドウで、すべてその情報を表示します。 それぞれのデバッガー ウィンドウには、ウィンドウに表示される情報のセットを制御するために選択できるタブがあります。 左側のデバッガー ウィンドウには、 **[ローカル]** 、 **[ウォッチ 1]** 、 **[ウォッチ 2]** 、 **[ウォッチ 3]** 、および **[ウォッチ 4]** の各タブがあります。 右側のデバッガー ウィンドウには、 **[呼び出し履歴]** 、 **[スレッド]** 、 **[ブレークポイント]** 、 **[コマンド ウィンドウ]** 、および **[出力]** の各タブがあります。  
  
> [!NOTE]  
>  前の説明は、デバッガー ウィンドウの既定の場所に適用されます。 タブは、ドラッグすることでウィンドウ間で移動できます。また、タブのドッキングを解除して新しいウィンドウを作成し、任意の場所に配置することもできます。  
  
 既定では、これらのタブまたはウィンドウの一部がアクティブになりません。 特定のウィンドウを開くには、次のどちらかの操作を行います。  
  
-   **[デバッグ]** メニューの **[ウィンドウ]** をクリックし、目的のウィンドウを選択する。  
  
-   **[デバッグ]** ツール バーの **[ブレークポイント]** をクリックし、目的のウィンドウを選択する。  
  
## <a name="transact-sql-expressions"></a>Transact-SQL 式  
 式は、変数やパラメーターなどの単独のスカラー値に評価される [!INCLUDE[tsql](../../includes/tsql-md.md)] 句です。 左側のデバッガー ウィンドウでは、式に現在割り当てられているデータ値を、最大で 5 つのタブまたはウィンドウに表示できます: **[ローカル]、[ウォッチ 1]** 、 **[ウォッチ 2]** 、 **[ウォッチ 3]** 、 **[ウォッチ 4]** です。  
  
 **[ローカル]** ウィンドウには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーの現在のスコープ内のローカル変数についての情報が表示されます。 **[ローカル]** ウィンドウに表示される式のセットは、一覧の式を追加または削除しない限り変更されません。  
  
 **[クイック ウォッチ]** と 4 つの **[ウォッチ]** ウィンドウに指定できる式は、変数の識別子だけではありません。 単一の値に評価される [!INCLUDE[tsql](../../includes/tsql-md.md)] 式 (変数に対して数値を加算する式など) や単一の値に評価される SELECT ステートメントを指定することができます。 たとえば、以下のような場合があります。  
  
-   変数の名前 (@IntegerCounter など)。  
  
-   変数に対する算術演算 (@IntegerCounter + 1 など)。  
  
-   2 つの文字変数に対する文字列操作 (@FirstName + @LastName など)。  
  
-   単一の値を返す SELECT ステートメント (SELECT CharCol FROM MyTable WHERE PrimaryKey = 1)。  
  
 **[クイック ウォッチ]** ウィンドウを使用すると、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 式の値を表示した後、その式を **[ウォッチ]** ウィンドウに保存できます。 **[クイック ウォッチ]** で式を選択するには、 **[式]** ボックスで式の名前を選択または入力します。  
  
 4 つの **[ウォッチ]** ウィンドウには、選択した変数および式に関する情報が表示されます。 **[ウォッチ]** ウィンドウに表示される式のセットは、一覧の式を追加または削除しない限り変更されません。  
  
 式を **[ウォッチ]** ウィンドウに追加するには、 **[クイック ウォッチ]** ダイアログ ボックスで **[ウォッチ式の追加]** を選択するか、または **[ウォッチ]** ウィンドウで空の行の **[名前]** 列に式の名前を入力します。  
  
 **[ローカル]** 、 **[ウォッチ]** 、または **[クイック ウォッチ]** の各ウィンドウで変数にデータ値を設定するには、行を右クリックし、 **[値の編集]** を選択します。 **[ローカル]** 、 **[ウォッチ]** 、および **[クイック ウォッチ]** ダイアログ ボックスの **[値]** 列では、テキスト、XML、および HTML のデータ ビジュアライザーがサポートされます。 ビジュアライザーは、 **[値]** 列の右側の虫眼鏡データ ヒントとして表されます。 ビジュアライザーを使用すると、データ型に一致するテキスト、XML、または HTML のデータ値を表示できます (たとえば、XML ファイルをブラウザー ウィンドウに表示できます)。  
  
 デバッグ モードでは、識別子の上にマウス ポインターを移動すると、式の名前とその現在の値が**クイック ヒント** ポップアップに表示されます。 詳細については、「[クイック ヒント &#40;IntelliSense&#41;](../../relational-databases/scripting/quick-info-intellisense.md)」を参照してください。  
  
## <a name="breakpoints"></a>ブレークポイント  
 **[ブレークポイント]** ウィンドウでは、現在設定されているブレークポイントを表示および管理できます。 詳細については、「 [Transact-SQL コードのステップ実行](../../relational-databases/scripting/step-through-transact-sql-code.md)」を参照してください。  
  
## <a name="call-stacks"></a>呼び出し履歴  
 **[呼び出し履歴]** ウィンドウには、現在の実行場所が表示されます。また、実行が元のエディター ウィンドウから [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュール (関数、ストアド プロシージャ、またはトリガー) 経由で現在の実行場所まで、どのように渡されたかについての情報も表示されます。 **[呼び出し履歴]** ウィンドウの各行はスタック フレームと呼ばれ、次のいずれかの項目を表します。  
  
-   現在の実行場所  
  
-   1 つのモジュールから別のモジュールへの呼び出し  
  
-   エディター ウィンドウから [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールへの呼び出し  
  
 スタックの順序は、モジュールが呼び出された順序の逆順になっています。 現在の実行場所はスタックの最上部に表示され、元の呼び出しは最下部に表示されます。 スタック フレームの左余白の黄色の矢印は、デバッガーが実行を一時停止したフレームを表します。  
  
 **[名前]** 列には、次の情報が記録されます。  
  
-   次のレベルへの呼び出しを行ったコード行を含む呼び出し元のモジュール。  
  
-   スタック上の次のモジュールを呼び出したコード行。  
  
-   パラメーターを受け取るストアド プロシージャまたは関数が呼び出された場合、すべてのパラメーターについて、名前、データ型、および値も表示されます。  
  
 **[ローカル]** 、 **[ウォッチ]** 、および **[クイック ウォッチ]** の各ウィンドウ内の式は、現在のスタック フレームに対して評価されます。 既定では、現在のスタック フレームは、デバッガーが実行を一時停止したスタック内の最上位のフレームです。 別のスタック フレームを現在のフレームとして指定した場合、 **[ローカル]** 、 **[ウォッチ]** 、および **[クイック ウォッチ]** の各ウィンドウ内の式は、新しいスタック フレームに対して再評価されます。 現在のスタック フレームを変更するには、フレームをダブルクリックするか、またはフレームをクリックし、 **[フレームに切り替え]** を選択します。 その時点で、 **[ローカル]** 、 **[ウォッチ]** 、および **[クイック ウォッチ]** の各ウィンドウ内の式が新しいフレームに対して再評価されます。 現在のスタック フレームがスタック内で最上位のフレームでない場合、現在のスタック フレームは、スタック フレームの左余白の緑色の矢印によって識別されます。  
  
 スタック フレームを右クリックし、 **[ソース コードへ移動]** を選択すると、そのフレームのコードがクエリ エディター ウィンドウに表示されます。 ただし、そのフレームは現在のフレームには設定されず、 **[ローカル]** 、 **[ウォッチ]** 、および **[クイック ウォッチ]** の各ウィンドウの内容も変更されません。  
  
## <a name="system-information-and-transact-sql-results"></a>システム情報および Transact-SQL の結果  
 **[出力]** ウィンドウには、デバッガーから出力される状態メッセージおよびイベント メッセージが表示されます。 たとえば、デバッガーがいつ他のプロセスにアタッチしたか、デバッガー スレッドがいつ終了したかなどの情報が表示されます。  
  
 デバッグ モードのとき、クエリ エディターの **[結果]** タブと **[メッセージ]** タブはアクティブ状態で維持されます。 **[結果]** タブには、デバッグ セッション中に実行された [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントからの結果セットが表示されます。 **[メッセージ]** タブには、システム メッセージ (たとえば " *xx* 行処理されました") や、PRINT ステートメントおよび RAISERROR ステートメントの出力が表示されます。  
  
## <a name="see-also"></a>参照  
 [[ローカル] ウィンドウ](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [[ウォッチ] ウィンドウ](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [[クイック ウォッチ] ダイアログ ボックス](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [[ブレークポイント] ウィンドウ](../../relational-databases/scripting/transact-sql-debugger-breakpoints-window.md)   
 [[呼び出し履歴] ウィンドウ](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [[スレッド] ウィンドウ](../../relational-databases/scripting/transact-sql-debugger-threads-window.md)   
 [[出力ウィンドウ]](../../relational-databases/scripting/transact-sql-debugger-output-window.md)   
 [Transact-SQL デバッガー](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
