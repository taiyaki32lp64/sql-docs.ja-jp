---
title: カーソルと準備されたステートメントでのトランザクションの影響 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 83b693922d08f7298d0c5282fe2c7d1c20149d5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046881"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>カーソルと準備されたステートメントでのトランザクションの影響
コミットまたはロールバック トランザクションにカーソルとアクセス プランで、次の影響はあります。  
  
-   すべてのカーソルは閉じられます、その接続で準備されたステートメント用のアクセス プランが削除されます。  
  
-   すべてのカーソルは閉じられ、その接続で準備されたステートメント用のアクセス プランがそのまま残ります。  
  
-   すべてのカーソルは開いたまま、その接続で準備されたステートメント用のアクセス プランがそのまま残ります。  
  
 たとえば、データ ソースはこの一覧は、これらの動作の最も厳しいの最初の動作を示します。 これで、アプリケーションは次の処理とします。  
  
1.  手動コミットのコミット モードを設定します。  
  
2.  ステートメントを 1 には、販売注文の結果セットを作成します。  
  
3.  ユーザーがその順序を強調表示したとき、2、ステートメントで販売注文の行の結果セットを作成します。  
  
4.  呼び出し**SQLExecute**ユーザーが行を更新するときに、3、ステートメントで準備されている位置指定の update ステートメントを実行します。  
  
5.  呼び出し**SQLEndTran**を位置指定の update ステートメントをコミットします。  
  
 データ ソースの動作への呼び出しにより**SQLEndTran**手順 5 を 1 と 2 のステートメントでカーソルを閉じると、すべてのステートメントにアクセス プランを削除すると、します。 アプリケーションは、1 と 2 を結果を再作成するステートメントのセットを再実行し、3 のステートメントでステートメントを再び準備する必要があります。  
  
 自動コミット モードでは、機能以外の**SQLEndTran**トランザクションのコミットします。  
  
-   **SQLExecute**または**SQLExecDirect**前の例への呼び出しで**SQLExecute**手順 4 がトランザクションをコミットします。 これにより、データ ソースを 1 と 2 のステートメントでカーソルを閉じて、その接続ですべてのステートメントのプランへのアクセスを削除します。  
  
-   **SQLBulkOperations**または**SQLSetPos**前の例では、たとえば、手順 4. で、アプリケーションを呼び出す**SQLSetPos**ステートメント 2 を実行する代わりに、SQL_UPDATE オプションを使用して、3 のステートメントで update ステートメントを配置します。 データ ソースが 1 と 2 は、ステートメントでカーソルをクローズして、その接続ですべてのアクセス プランを破棄このトランザクションをコミットします。  
  
-   **SQLCloseCursor**前の例では、たとえば、ユーザーは、別の販売注文を強調表示、ときに、アプリケーションが呼び出す**SQLCloseCursor**新しい売上の明細行の結果を作成する前にステートメント 2順序。 呼び出し**SQLCloseCursor**コミット、**SELECT**行の結果セットを作成し、データ ソースが、1 ステートメントでカーソルを閉じ、上のすべてのアクセス プランを破棄するステートメント接続します。  
  
 アプリケーション、特にスクリーン ベースのアプリケーションでユーザーが、結果セットと更新プログラムの周囲をスクロールまたは行の削除は、この問題をコードに注意してくださいである必要があります。  
  
 トランザクションがコミットまたはロールバック時のデータ ソースの動作を決定するには、アプリケーションを呼び出す**SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR および SQL_CURSOR_ROLLBACK_BEHAVIOR のオプションを使用します。
