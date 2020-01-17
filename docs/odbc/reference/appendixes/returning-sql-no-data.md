---
title: SQL_NO_DATA を返す |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2613593d9c2e20d5dfa01c0a0b4f9886dbc8e889
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057133"
---
# <a name="returning-sqlnodata"></a>SQL_NO_DATA を返す
ときに、ODBC *2.x*アプリケーションを処理する ODBC *3.x*ドライバー呼び出し**SQLExecDirect**、 **SQLExecute**、または**SQLParamData**、検索された update または delete ステートメントが実行されましたが、ODBC データ ソースの行によって影響されなかったと*3.x*ドライバーは SQL_SUCCESS を返す必要があります。 ときに、ODBC *3.x* odbc 作業アプリケーション*3.x*ドライバー呼び出し**SQLExecDirect**、 **SQLExecute**、または**SQLParamData**と同じ結果が、ODBC *3.x*ドライバーが SQL_NO_DATA を返す必要があります。  
  
 ステートメントのバッチにし、データ ソースで行が削除されない場合は、検索結果の update または delete のステートメント**SQLMoreResults** SQL_SUCCESS を返します。 SQL_NO_DATA は、するものであり、検索された更新/削除する行が影響を受けませんからの結果は、以上結果があることを意味するために返すことはできません。
