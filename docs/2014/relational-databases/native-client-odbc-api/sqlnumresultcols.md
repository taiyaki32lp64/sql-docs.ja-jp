---
title: SQLNumResultCols |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c1a4825dc8d73f815f6b399c6e3a51c064d3b9b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424321"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  実行されるステートメントを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC ドライバーは結果セット内の列の数を報告するサーバーを利用しません。 この場合、`SQLNumResultCols`サーバーとのやり取りは行われません。 ような[SQLDescribeCol](sqldescribecol.md)と[SQLColAttribute](sqlcolattribute.md)を呼び出すと、`SQLNumResultCols`準備されていても実行されていないステートメントには、サーバーとのやり取りが生成されます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントまたはステートメント バッチが複数の結果行セットを返すときは、結果セットの列数を報告する場合、あるセットから別のセットへ結果セットを変更することができます。 `SQLNumResultCols` 各セットに対して呼び出す必要があります。 列数が変化すると、アプリケーションでは行の結果をフェッチする前に、データ値を再バインドする必要があります。 セットを返す複数の結果の処理の詳細についてを参照してください[SQLMoreResults](sqlmoreresults.md)します。  
  
 以降では、データベース エンジンの機能強化[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]期待どおりの結果のより正確な記述を取得する SQLNumResultCols を許可します。 これらのより正確な結果の以前のバージョンの SQLNumResultCols によって返される値が異なる場合があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。[メタデータ検出](../native-client/features/metadata-discovery.md)します。  
  
## <a name="see-also"></a>参照  
 [SQLNumResultCols 関数](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  