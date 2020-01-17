---
title: データベース オブジェクトの使用 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5bf11ece3797f9bbc580339846efb685876b2d0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188625"
---
# <a name="working-with-database-objects"></a>データベース オブジェクトでの作業
  SMO オブジェクトの作成には次の段階があります。  
  
1.  オブジェクトのインスタンスの作成。  
  
2.  オブジェクト プロパティの設定。  
  
3.  子オブジェクトのインスタンスの作成。  
  
4.  子オブジェクト プロパティの設定。  
  
5.  オブジェクトの作成。  
  
 SMO アプリケーションで SMO オブジェクトのインスタンスを作成する場合、`Create` メソッドが発行されるまでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンス上にこれらのインスタンスが存在しません。 ただし、個々のオブジェクトに対して `Create` メソッドを発行する必要はありません。 オブジェクトに一連の子オブジェクトがある場合、`Create` メソッドを実行するには親オブジェクトのみが必要となります。 たとえば、テーブルの定義には、テーブルに含まれている列が 1 つ以上必要になります。 一方、テーブルがなくては列が独立して存在することはできません。 テーブルとテーブルの列の間には共存関係があります。  
  
 <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> メソッドを使用すると、オブジェクトへの変更を行うことができます。 オブジェクト コレクションの 1 つへの子オブジェクトの追加や、プロパティ値の変更など、1 つのオブジェクトに対する複数の変更は、バッチ化されて 1 つの変更として実行されます。 `Alter` メソッドを使用することによって、ネットワーク トラフィックが減少し、全体のパフォーマンスが向上します。  
  
 オブジェクトを削除するには、`Drop` ステートメントを使用します。このとき、そのオブジェクトの初期作成時に要した、共存関係にある子オブジェクトもすべて削除されます。  
  
## <a name="see-also"></a>参照  
 [SMO オブジェクト モデル](../smo-object-model.md)  
  
  
