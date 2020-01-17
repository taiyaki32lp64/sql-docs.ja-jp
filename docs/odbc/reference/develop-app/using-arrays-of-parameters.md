---
title: パラメーターの配列の使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf6b5127bac7aedf9e67918d38020c73a4afe186
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079599"
---
# <a name="using-arrays-of-parameters"></a>パラメーターの配列の使用
アプリケーションの呼び出しのパラメーターの配列を使用する**SQLSetStmtAttr**で、*属性*SQL_ATTR_PARAMSET_SIZE パラメーター セットの数を指定する引数。 呼び出す**SQLSetStmtAttr**で、*属性*SQL_ATTR_PARAMS_PROCESSED_PTR ドライバーが処理された、パラメーターのセットの数を返すことができます、変数のアドレスを指定の引数などのエラーを設定します。 呼び出す**SQLSetStmtAttr**で、*属性*でパラメーター値の行ごとに状態情報を返す配列を指す SQL_ATTR_PARAM_STATUS_PTR の引数。 ドライバーは、ステートメントを保持する構造体でこれらのアドレスを格納します。  
  
> [!NOTE]  
>  ODBC 2。*x*、 **SQLParamOptions**パラメーターに複数の値を指定するが呼び出されました。 ODBC 3。*x*への呼び出し**SQLParamOptions**への呼び出しによって置き換えられました**SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE と SQL_ATTR_PARAMS_PROCESSED_ARRAY 属性を設定するには.  
  
 ステートメントを実行する前に、アプリケーションは、各バインドの配列の各要素の値を設定します。 ドライバーがパラメーター値を取得し、データ ソースに送信する、格納されている情報を使用して、ステートメントが実行されたときに可能であれば、ドライバーは、配列としてこれらの値を送信する必要があります。 パラメーターの配列の使用はデータ ソースに単一の呼び出しで、配列内のすべてのパラメーターを含む SQL ステートメントを実行することによっては最適に実装され、この機能が Dbms で広く利用可能な今日は ただし、ドライバーをシミュレートできますがそれぞれ 1 つのパラメーターと共に SQL ステートメント、複数回の実行します。  
  
 アプリケーションでは、パラメーターの配列を使用する前に、アプリケーションで使用される、ドライバーでサポートされていることを確認が必要があります。 これには 2 つの方法があります。  
  
-   パラメーターの配列をサポートするドライバーだけを使用します。 アプリケーションがハードコードされたこれらのドライバーの名前またはユーザーがこれらのドライバーのみを使用するように指示することができます。 カスタム アプリケーションと垂直方向のアプリケーションは、通常、制限付きの一連のドライバーを使用します。  
  
-   実行時にパラメーターの配列のサポートを確認します。 ドライバーは、SQL_ATTR_PARAMSET_SIZE ステートメント属性を 1 より大きい値に設定する可能性がある場合、パラメーターの配列をサポートします。 汎用アプリケーション、および垂直方向のアプリケーションのパラメーターの配列のサポートをよく、確認の実行時にします。  
  
 行の数とパラメーター化された実行の結果セットの可用性を呼び出すことによって決まりますできます**SQLGetInfo** SQL_PARAM_ARRAY_ROW_COUNTS および SQL_PARAM_ARRAY_SELECTS のオプションを使用します。 **挿入**、 **UPDATE**、および**削除**個々 の行の数 (パラメーターのセットごとに 1 つ) がいるかどうかを示すステートメント、SQL_PARAM_ARRAY_ROW_COUNTS オプション使用可能な (SQL_PARC_BATCH) または行をカウントするかどうかは、(SQL_PARC_NO_BATCH) いずれかにロールアップされます。 **選択**ステートメント、SQL_PARAM_ARRAY_SELECTS オプションは、結果セットが (SQL_PAS_BATCH) のパラメーターのセットごとに使用できるかどうか、または 1 つの結果セットの使用可能な (SQL_PAS_NO_BATCH) がかどうかを示します。 ドライバーがパラメーターの配列を実行するときに結果セットを生成するステートメントを許可していない場合、SQL_PARAM_ARRAY_SELECTS は SQL_PAS_NO_SELECT を返します。 これらのステートメントでパラメーターの使用のデータ ソースに固有と ODBC SQL 文法を行いませんがため、特に、ステートメントは、他の種類とパラメーターの配列を使用できるかどうかのデータ ソースに固有になります。  
  
 SQL_ATTR_PARAM_OPERATION_PTR ステートメント属性によって示される配列は、パラメーターの行を無視できます。 その要素に対応するパラメーターのセットがから除外して、配列の要素が SQL_PARAM_IGNORE に設定されている場合、 **SQLExecute**または**SQLExecDirect**呼び出します。 SQL_ATTR_PARAM_OPERATION_PTR 属性によって示される配列が割り当てられ、アプリケーションによって、ドライバーによって読み取られました。 フェッチされる行を入力パラメーターとして使用する場合は、パラメーターの操作の配列内の行の状態の配列の値を使用できます。  
  
## <a name="error-processing"></a>エラー処理  
 ステートメントの実行中にエラーが発生した場合、実行関数はエラーが返され、エラーを含む行の数に行番号の変数を設定します。 ただし、エラー設定を実行またはエラー セットが実行されます (ただし、期間の終了時刻) の前にすべての行かどうか、すべての行かどうかデータ ソースに固有になります。 パラメーターのセットが処理されるため、ドライバーは現在処理されている行の数、SQL_ATTR_PARAMS_PROCESSED_PTR ステートメント属性で指定したバッファーを設定します。 すべてのセット エラー セットが実行される点を除いて場合、ドライバーはすべての行が処理された後、SQL_ATTR_PARAMSET_SIZE にこのバッファーを設定します。  
  
 SQL_ATTR_PARAM_STATUS_PTR ステートメント属性が設定されている場合**SQLExecute**または**SQLExecDirect**を返します、*パラメーター状態配列、* 状態を提供します。各パラメーターのセット。 パラメーター状態配列は、アプリケーションによって割り当てられ、ドライバーによっては。 その要素は、パラメーターの行に、SQL ステートメントを正常に実行されたかどうか、またはパラメーターのセットを処理中にエラーが発生したかどうかを示します。 エラーが発生した場合、ドライバーは SQL_PARAM_ERROR パラメーター状態配列内の対応する値を設定し、SQL_SUCCESS_WITH_INFO が返されます。 アプリケーションでは、どの行が処理されたかを判断する状態配列を確認できます。 行番号を使用して、アプリケーションできる多くの場合、エラーを修正して処理を再開します。  
  
 パラメーターの状態配列を使用する方法はへの呼び出しによって返される SQL_PARAM_ARRAY_ROW_COUNTS と SQL_PARAM_ARRAY_SELECTS オプションによって決まります**SQLGetInfo**します。 **挿入**、 **UPDATE**、および**削除**SQL_PARAM_ARRAY_ SQL_PARC_BATCH が返されます場合、ステータス情報を使用してステートメントをパラメーター状態配列が入力されますROW_COUNTS、SQL_PARC_NO_BATCH が返される場合に適しません。 **選択**ステートメント パラメーター状態配列に挿入 SQL_PARAM_ARRAY_SELECT、SQL_PAS_BATCH が返されますが、SQL_PAS_NO_BATCH または SQL_PAS_NO_SELECT が返された場合にありません。  
  
## <a name="data-at-execution-parameters"></a>実行時データ パラメーター  
 長さ/インジケーター配列内の値のいずれかが生成される場合や、SQL_LEN_DATA_AT_EXEC の結果である場合 (*長さ*) これらの値のデータが送信されるマクロ、 **SQLPutData**通常の方法でします。 このプロセスの次の側面は、すぐに明らかではないために特殊なコメントをしてください。  
  
-   ドライバーには、SQL_NEED_DATA が返される、ときにが必要なデータの行に行番号の変数のアドレスを設定があります。 1 つの値を持つように、アプリケーションは、ドライバーがパラメーターの 1 つのセット内のパラメーター値を要求する順序についてどのような想定をことはできません。 SQL_ATTR_PARAMS_PROCESSED_PTR ステートメント属性で指定したバッファーが、エラーが発生するで指定された行の状態配列内の行の状態の行の番号に設定されて実行時データ パラメーターの実行でエラーが発生する場合また、SQL_ATTR_PARAM_STATUS_PTR ステートメント属性は SQL_PARAM_ERROR とへの呼び出しに設定されて**SQLExecute**、 **SQLExecDirect**、 **SQLParamData**、または**SQLPutData** SQL_ERROR を返します。 このバッファーの内容は定義されていない場合は**SQLExecute**、 **SQLExecDirect**、または**SQLParamData** SQL_STILL_EXECUTING を返します。  
  
-   ドライバーでの値が解釈されないため、 *ParameterValuePtr*の引数**SQLBindParameter**アプリケーションは、配列へのポインターを提供する場合、実行時データ パラメーターの**SQLParamData**はいない抽出し、この配列の要素をアプリケーションに返します。 代わりに、スカラー値、アプリケーションが提供を返します。 つまり、によって返される値**SQLParamData**データの送信に必要なアプリケーションを対象のパラメーターを指定する十分なは、アプリケーションは、現在の行の数を検討することも必要があります。  
  
     ときにだけいくつかのパラメーターの配列の要素が、実行時データ パラメーターで、アプリケーション渡す必要があります、配列内のアドレス*ParameterValuePtr*要素のすべてのパラメーターを格納します。 この配列は通常の実行時データ パラメーターではないパラメーターに解釈されます。 実行時データ パラメーターの値を**SQLParamData**には、通常どおりに使用できるこの機会に、ドライバーが要求しているデータを識別するために、アプリケーションは、配列のアドレスでは常に。
