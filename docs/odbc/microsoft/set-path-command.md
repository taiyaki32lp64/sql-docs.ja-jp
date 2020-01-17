---
title: SET PATH コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57685731bc5eb86381816d0cbb91a4942b5bfeff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063645"
---
# <a name="set-path-command"></a>SET PATH コマンド
ファイルの検索のパスを指定します。 ドライバー固有の情報は、「解説」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>引数  
 [*パス*]  
 Visual FoxPro を検索するディレクトリを指定します。 コンマまたはセミコロンを使用して、ディレクトリを区切ります。  
  
## <a name="remarks"></a>コメント  
 パスの設定では、ストアド プロシージャ内で呼び出すことができるその他の Visual FoxPro プログラムの検索パスを指定できます。 パスの設定では、接続の指定したデータ ソースのパスは変更されません。  
  
 せずパスに設定を発行*パス*既定のディレクトリまたはフォルダーへのパスを復元します。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 ストアド プロシージャにパスの設定を発行した場合は、次の関数やコマンドによって無視されます。  
  
-   カタログ関数をなど[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)と[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)は、新しいパスを無視し、内のデータ ソースで指定されたパスを参照する続行[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)または[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)します。  
  
-   SELECT、INSERT、UPDATE、DELETE、および CREATE TABLE などのコマンドは、新しいパスを無視して続行内のデータ ソースで指定されたパスを参照する**SQLPrepare**または**SQLExecDirect**します。  
  
 ストアド プロシージャにパスの設定を発行してその元の状態に、その後、パスを設定しないでください (パスの設定のスコープはデータのセッションにしない) ため、データベースへの接続は、新しいパスを使用します。  
  
 作成、選択、またはデータ ソースで指定されている以外のディレクトリ内のテーブルを更新する場合、コマンドを使用して、ファイルの完全なパスを指定します。  
  
## <a name="see-also"></a>関連項目  
 [ODBC Visual FoxPro セットアップ ダイアログ ボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Visual FoxPro ODBC ドライバー)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro ODBC ドライバー)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Visual FoxPro ODBC ドライバー)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
