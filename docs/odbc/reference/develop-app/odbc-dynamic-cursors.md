---
title: ODBC 動的カーソル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 628de07f90de47efb0546dff84c03f56efb0674c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086297"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 動的カーソル
動的カーソルがあっただけです。 動的です。 メンバーシップ、順序、および、カーソルを開いた後に結果セットの値に加えられた変更を検出できます。 たとえば、動的カーソルで 2 つの行がフェッチされた後、別のアプリケーションによって一方の行は更新され、他の行は削除されたものとします。 動的カーソルは、行の再フェッチしようとすると、削除された行は見つかりませんが、更新された行の新しい値を返します。  
  
 動的カーソルは、すべての更新プログラムを検出削除、および挿入する場合に、どちらも、自分と他のユーザーによるものです。 (これは、分離の対象 SQL_ATTR_TXN_ISOLATION 接続属性によって設定されると、トランザクションのレベル) です。SQL_ATTR_ROW_STATUS_PTR ステートメント属性で指定された行の状態配列では、これらの変更を反映し、SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、SQL_ROW_ERROR、SQL_ROW_UPDATED、および SQL_ROW_ADDED に含めることができます。 動的カーソルが行セット外の削除された行は返されません、そのため、結果セットで削除された行または行の状態配列内の対応する要素の存在を認識しないために、SQL_ROW_DELETED を戻すことはできません。 呼び出しによって行が更新された場合にのみ、SQL_ROW_ADDED が返される**SQLSetPos**別のカーソルによって更新されたときではなく、します。  
  
 データベースに動的カーソルを実装する方法の 1 つのメンバーシップを定義する選択的インデックスを作成して、結果の順序によって設定されます。 他のユーザーの変更時にインデックスが更新されるため、このようなインデックスに基づくカーソルは、すべての変更。 このインデックスで定義された結果セット内の他の項目は、インデックスに沿った処理によって可能性があります。  
  
 動的カーソルは、一意のキー順に並べ替えられますに結果セットを要求することによってシミュレートできます。 このような制限は、フェッチが実行することによって行われた、**選択**ステートメントごとに、カーソルに行がフェッチされます。 たとえば、このステートメントによって結果セットが定義されているとします。  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 この結果セット内の次の行セットをフェッチするには、シミュレートされたカーソルでは、次のパラメーターを設定**選択**ステートメントは、現在の行セットの最後の行の値にしを実行します。  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 このステートメントは、Customers テーブルに 2 つ目の結果セットを最初の行セットは、この例では、元の結果セット内の次の行セットが、行のセットを作成します。 カーソルは、アプリケーションにこの行セットを返します。  
  
 興味深いは、この方法で実装される動的カーソルは、多くの結果セットを実際に作成して元の結果セットの変更を検出することができます。 アプリケーションはこれら補助の結果セットの存在を学習します。カーソルが元の結果セットへの変更を検出できない場合は、単が表示されます。
