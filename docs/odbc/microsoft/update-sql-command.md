---
title: UPDATE - SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0230329d10d2414724379d4b9d38c4851a031bca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912333"
---
# <a name="update---sql-command"></a>UPDATE - SQL コマンド
新しい値では、テーブル内のレコードを更新します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブの Visual FoxPro 言語の構文をサポートしています。 ドライバー固有の情報を参照してください。**ドライバー解説**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>引数  
 UPDATE [ *DatabaseName1!* ] *TableName1*  
 新しい値を持つレコードを更新するテーブルを指定します。  
  
 *DatabaseName1!* テーブルを含むデータ ソースで指定されたデータベース以外のデータベースの名前を指定します。 データベースで現在ない場合は、テーブルを含むデータベースの名前を含める必要があります。 データベース名の後に、テーブル名の前に感嘆符 (!) 区切り記号が含まれます。  
  
 設定*Column_Name1*= *eExpression1*[、 *Column_Name2*= *eExpression2*  
 更新される列とその新しい値を指定します。 WHERE 句を省略した場合は、同じ値を持つ列のすべての行が更新されます。  
  
 場所*FilterCondition1*[AND&#124;または*FilterCondition2*...]  
 新しい値で更新されるレコードを指定します。  
  
 *FilterCondition*に新しい値で更新するレコードが満たす必要のある条件を指定します。 AND で接続して、好きな数のフィルター条件を含めることができますか、OR 演算子。 NOT 演算子を使用して、論理式の値を反転するかを使用することができます**空**空のフィールドを確認する ()。  
  
## <a name="remarks"></a>コメント  
 UPDATE - SQL は、1 つのテーブルのレコードだけを更新できます。  
  
 UPDATE - SQL は置換 とは異なり、テーブル内の複数のレコードを更新共有アクセスで開かれたときにレコードがロックを使用します。 これにより、マルチ ユーザーの状況でレコードの競合が減少が、パフォーマンスが低下することができます。 パフォーマンスを最大にするには、テーブルを開くことの排他的使用または使用**群れ**テーブル ロック ()。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションでは、ODBC SQL ステートメントの更新をデータ ソースに送信するときに、Visual FoxPro ODBC ドライバーを翻訳しないで Visual FoxProUPDATE コマンドに、コマンドに変換します。  
  
## <a name="see-also"></a>関連項目  
 [DELETE - SQL コマンド](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL コマンド](../../odbc/microsoft/insert-sql-command.md)
