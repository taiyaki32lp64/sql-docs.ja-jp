---
title: INSERT - SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 884a33339db10ee8e07d8b432d1765720d45734a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019453"
---
# <a name="insert---sql-command"></a>INSERT - SQL コマンド
指定されたフィールドの値を含むテーブルの末尾にレコードを追加します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブの Visual FoxPro 言語の構文をサポートしています。 ドライバー固有の情報は、「解説」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>引数  
 INSERT INTO *dbf_name*  
 新しいレコードを追加するテーブルの名前を指定します。 *dbf_name*パスを含めることができ、名前の式を指定できます。  
  
 指定したテーブルが開いていない場合は、新しい作業領域でのみが開かれ、新しいレコードがテーブルに追加されます。 新しい作業領域が選択されていません。現在の作業領域では、選択されたままです。  
  
 指定したテーブルが開いている場合は、INSERT、テーブルに新しいレコードを追加します。 現在の作業領域以外にテーブルが作業領域で開く場合は、選択されていない後、レコードが追加されます。現在の作業領域では、選択されたままです。  
  
 [( *fname1*[, *fname2*[, ...]])]  
 新しいレコードのフィールドの名前を指定しますに値が挿入されます。  
  
 VALUES ( *eExpression1*[, *eExpression2*[, ...]])  
 新しいレコードに挿入されたフィールドの値を指定します。 フィールド名を省略した場合は、テーブル構造で定義された順序でフィールド値を指定する必要があります。  
  
## <a name="remarks"></a>コメント  
 新しいレコードには、VALUES 句で表示されているデータが含まれています。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションは、ODBC SQL ステートメントの INSERT をデータ ソースに送信するときに、Visual FoxPro ODBC ドライバーを翻訳しないで Visual FoxProINSERT コマンドに、コマンドに変換します。  
  
## <a name="see-also"></a>関連項目  
 [CREATE TABLE - SQL コマンド](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL コマンド](../../odbc/microsoft/select-sql-command.md)
