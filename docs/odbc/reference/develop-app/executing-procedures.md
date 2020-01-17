---
title: プロシージャの実行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c36f02bde63862748eef14a8cbae063ca4e472
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069951"
---
# <a name="executing-procedures"></a>プロシージャの実行
ODBC では、プロシージャを実行するための標準のエスケープ シーケンスを定義します。 このシーケンスおよびそれを使用するコード例の構文を参照してください。[プロシージャ呼び出し](../../../odbc/reference/develop-app/procedure-calls.md)します。  
  
 プロシージャを実行するには、アプリケーションは、次の操作を実行します。  
  
1.  パラメーターの値を設定します。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。  
  
2.  呼び出し**SQLExecDirect**プロシージャを実行する SQL ステートメントを含む文字列を渡します。 このステートメントは、ODBC または DBMS 固有の構文で定義されているエスケープ シーケンスを使用できます。DBMS に固有の構文を使用するステートメントは相互運用可能ではありません。  
  
3.  ときに**SQLExecDirect**を呼び出すと、ドライバー。  
  
    -   現在のパラメーター値を取得し、必要に応じてそれらを変換します。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。  
  
    -   データ ソース内のプロシージャを呼び出すし、変換されたパラメーターの値を送信します。 ドライバーが、プロシージャを呼び出す方法と、ドライバー固有です。 たとえば、データ ソースの SQL 文法を使用し、実行するためには、このステートメントを送信する SQL ステートメントを変更する可能性があります。 または DBMS のデータ ストリーム プロトコルで定義されているリモート プロシージャ コール (RPC) メカニズムを使用して直接プロシージャを呼び出すことができます。  
  
    -   入力/出力または出力パラメーターの値またはプロシージャが成功したと仮定すると、プロシージャの戻り値を返します。 これらの値は、他すべての結果 (行数と結果セット)、プロシージャによって生成されたが処理された後まで使用できない可能性があります。 プロシージャが失敗した場合、ドライバーはエラーを返します。
