---
title: ファイル ベースのドライバー診断の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23234a490f664c4be0811152b2b77ae7c0b73761
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069833"
---
# <a name="file-based-driver-diagnostic-example"></a>ファイル ベースのドライバー診断の例
ファイル ベースのドライバーは、ODBC ドライバー、およびデータ ソースとして機能します。 ODBC 接続では、データ ソースとして、したがってエラーと警告の両方のコンポーネントとしてを生成ができます。 書式設定し、引数を返します、ドライバー マネージャーとのインターフェイスのコンポーネントもはであるため**SQLGetDiagRec**します。  
  
 たとえば、dbase Microsoft® driver driver は、十分なメモリを割り当てられませんでしたが返す可能性があります、次の値から**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 このエラーに関連するデータ ソースがありません、ため、ドライバーにのみ追加プレフィックス診断メッセージ ([Microsoft]) のベンダーとドライバー ([ODBC dBASE ドライバー])。  
  
 ドライバー Employee.dbf ファイルが見つかりませんでした、次の値を返す可能性があります**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 このエラーは、データ ソースに関連するが、ために、ドライバーをプレフィックスとして ([dBASE]) のデータ ソースのファイル形式を診断メッセージを追加しました。 ドライバーでデータ ソースと接続コンポーネントもあるために、仕入先 ([Microsoft]) およびドライバー ([ODBC dBASE ドライバー]) のプレフィックスが追加されます。
