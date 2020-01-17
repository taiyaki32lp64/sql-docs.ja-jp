---
title: 付録 B:ODBC の状態遷移テーブル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ceb128aec3a4cbe5ef7180483eb2a033ae57138
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996244"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>付録 B:ODBC の状態遷移テーブル
この付録の内容の表では、ODBC 関数による環境、接続、ステートメント、および記述子の状態の遷移の発生を示しています。 通常、環境、接続、ステートメント、または記述子の状態は、ハンドル (環境、接続、ステートメント、または記述子) の対応する型を使用する関数を呼び出すことがときにによって決まります。 次の図に示すようにほぼ重複する環境、接続、ステートメント、および記述子の状態。 たとえば、接続の正確な重複を示す C5、C6、S1 S12 からされているデータ ソースに依存する、異なるデータ ソースの場合は、異なる時刻でトランザクションが開始し、記述子の状態 (暗黙的に割り当てられた記述子) D1i 依存ためにについてはステートメント記述子が関連付けられているステートメントの状態、状態 (明示的に割り当てられた記述子) D1e 中には任意のステートメントの状態の独立したです。 各状態の説明は、次を参照してください[環境遷移](../../../odbc/reference/appendixes/environment-transitions.md)、[接続の遷移](../../../odbc/reference/appendixes/connection-transitions.md)、[ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md)、および[記述子の遷移。](../../../odbc/reference/appendixes/descriptor-transitions.md)、この付録で後述します。  
  
 環境と接続の状態は次のとおり重複します。  
  
 ![環境と接続の状態の重複](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 接続とステートメントの状態は次のとおり重複します。  
  
 ![インジケーター状態の接続とステートメント](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 次のように重複するステートメントと記述子の状態。  
  
 ![インジケーター状態のステートメントと記述子](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 接続と記述子の状態は次のとおり重複します。  
  
 ![インジケーター状態の接続と記述子](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 移行テーブル内の各エントリには、次の値のいずれかを指定できます。  
  
-   **--** のこの関数を実行した後状態は変更されません。  
  
-   **E**  

     **_n_**  、 **C_n_** 、 **S_n_** 、または**D_n_** -環境、接続、ステートメント、または記述子の状態が、指定した状態に移動します。  
 
-   **(組み込み)** -無効なハンドルは、関数に渡されました。 場合は、ハンドルが null のハンドルか、間違った型の有効なハンドルなど、接続ハンドルときに渡されたステートメント ハンドルが必要であった SQL_INVALID_HANDLE; を返しますそれ以外の場合の動作は未定義と致命的な可能性があります。 指定した状態で、関数の呼び出しの可能な唯一の結果がある場合にのみ、このエラーが表示されます。 このエラーは、状態は変更されませんし、かっこで示されますが、ドライバー マネージャーによって常に検出します。  
  
-   **NS** -次の状態。 ステートメントの移行では、非同期状態をステートメントが完了していない場合と同じです。 たとえば、結果セットを作成するステートメントが状態になる S11 状態 S1 からため**SQLExecDirect** SQL_STILL_EXECUTING が返されます。 状態 S11 NS 表記では、ステートメントの遷移と同じ状態 S1 内のステートメントの結果セットを作成することを意味します。 場合**SQLExecDirect**エラーが返された状態 S1 のまま、ステートメント;、ステートメントが S5 の状態に移動します成功すると、;、ステートメントが S8; の状態に移動してデータを必要がある場合とがまだ実行している場合 S11 の状態のままにします。  

-   **_XXXXX_** または **(*XXXXX*)** - 遷移のテーブルに関連付けられている SQLSTATEドライバー マネージャーによって検出された SQLSTATEs はかっこで囲まれています。 SQL_ERROR と指定の SQLSTATE 関数が返されますが、状態は変わりません。 たとえば場合、 **SQLExecute**前に呼び出されます**SQLPrepare**、SQLSTATE HY010 を返します (関数のシーケンス エラーです)。  

> [!NOTE]  
>  テーブルでは、状態を変更しない移行テーブルに関連しないエラーが表示されません。 たとえば、 **SQLAllocHandle** E1 環境の状態で呼び出され、SQLSTATE HY001 を返します (メモリ割り当てエラー) E1 の状態は、環境のままですこれについては、環境の遷移表では表示されません **。SQLAllocHandle**します。  
  
 環境、接続、ステートメント、または記述子が 1 つ以上の状態に移動できる場合、は、考えられる各状態が表示され、1 つまたは複数の脚注を各遷移が行われる条件を説明します。 任意のテーブルでは、次の脚注が表示されます。  
  
|脚注|説明|  
|--------------|-------------|  
|b|前に、または後にします。 または、結果セットの終了後に結果セットの開始前に、カーソルが配置されました。|  
|c|現在の関数。 現在の関数は非同期的に実行しています。|  
|d|データを必要があります。 関数には、SQL_NEED_DATA が返されます。|  
|e|エラー状態。 関数には、SQL_ERROR が返されます。|  
|i|行が無効です。 カーソルが位置していたセットといずれかの行を削除されましたが、結果内の行または行の操作でエラーが発生しました。 行の状態配列が存在する場合は、行の行の状態配列内の値は SQL_ROW_DELETED、SQL_ROW_ERROR またはでした。 (行の状態配列を指していますし、SQL_ATTR_ROW_STATUS_PTR ステートメントの属性です。)|  
|nf|見つかりませんでした。 関数には、SQL_NO_DATA が返されます。 ときにこれは当てはまりません**SQLExecDirect**、 **SQLExecute**、または**SQLParamData** sql_no_data が、検索を実行した後の update または delete ステートメント。|  
|np|準備されていません。 ステートメントは準備されていません。|  
|nr|結果はありません。 ステートメントは、しませんまたは、結果セットを作成できませんでした。|  
|o|その他の関数。 別の関数は非同期的に実行しています。|  
|p|準備します。 ステートメントが準備されています。|  
|r|結果。 または (場合によっては空) の結果セットを作成してステートメントです。|  
|s|成功。 関数には、SQL_SUCCESS_WITH_INFO または SQL_SUCCESS が返されます。|  
|v|有効な行です。 カーソルが結果セット内の行に配置されていると、行が正常に挿入されると、正常に更新または行に対する別の操作が正常に完了しました。 行の状態配列が存在する場合は、行の行の状態配列内の値は SQL_ROW_ADDED、SQL_ROW_SUCCESS、または SQL_ROW_UPDATED でした。 (行の状態配列を指していますし、SQL_ATTR_ROW_STATUS_PTR ステートメントの属性です。)|  
|○|実行中。 関数には、SQL_STILL_EXECUTING が返されます。|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 この例では、環境の状態遷移の行の表の**SQLFreeHandle**とき*HandleType* sql_handle_env としては、次のようには、します。  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|(組み込み)|E0|(HY010)|  
  
 場合**SQLFreeHandle**環境状態 E0 で呼び出される*HandleType* SQL_INVALID_HANDLE が返されないドライバー マネージャーを sql_handle_env としてに設定します。 E1 の状態で呼び出された場合*HandleType* E0 状態の場合は、関数が成功し、関数が失敗した場合に、E1 の状態のままに、環境を移動を sql_handle_env としてに設定します。 E2 の状態で呼び出された場合*HandleType*を SQL_HANDLE_ENV 設定、ドライバー マネージャーは、常に返します SQL_ERROR と SQLSTATE HY010 (関数のシーケンス エラーです)、環境が E2 の状態を維持します。  
  
 状態遷移のテーブルを理解するのを参照している (環境、接続、ステートメント、または記述子) は、どの項目を理解する必要があります。 関数 X の種類のアイテムのハンドルを受け取るとします。その関数 X の状態遷移表では、どの呼び出し元関数 X の種類のアイテムのハンドルを使用して影響その項目について説明します。 たとえば、 **SQLDisconnect**接続ハンドルを受け取ります。 接続の状態遷移表**SQLDisconnect**について説明する方法**SQLDisconnect**呼び出されますが、接続の状態に影響します。  
  
 関数は、Y が X と等しく、Y の種類のアイテムのハンドルを受け取るとします。その関数 X の状態遷移表では、どの呼び出し元関数、Y、型の項目に関連付けられている型のハンドルを持つ影響 Y の型の項目について説明します。たとえば、ステートメントの状態遷移表の**SQLDisconnect**について説明する方法**SQLDisconnect**を持つ接続のハンドルを使用して呼び出されたときに、ステートメントの状態に影響しますステートメントは、関連付けられています。  
  
 この付録には、次のトピックが含まれています。  
  
-   [環境の遷移](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [接続の遷移](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [記述子の遷移](../../../odbc/reference/appendixes/descriptor-transitions.md)
