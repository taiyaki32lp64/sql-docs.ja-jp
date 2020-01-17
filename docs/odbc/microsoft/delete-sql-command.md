---
title: DELETE - SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79a9c9a86e290f568f205a7e7678122f9089a7e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096331"
---
# <a name="delete---sql-command"></a>DELETE - SQL コマンド
レコードの削除をマークします。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブの Visual FoxPro 言語の構文をサポートしています。 ドライバー固有の情報は、「解説」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>引数  
 FROM [ *DatabaseName!* ] *TableName*  
 レコードが削除対象としてマークするテーブルを指定します。  
  
 *DatabaseName!* 包含データベースは、データ ソースと指定されたデータベースがない場合は、テーブルを含むデータベースの名前を指定します。 データベースが、データ ソースと指定されたデータベースではない場合は、テーブルを含むデータベースの名前を含める必要があります。 データベース名の後に、テーブル名の前に感嘆符 (!) 区切り記号が含まれます。  
  
 場所*FilterCondition1*[AND&#124;または*FilterCondition2*...]  
 Visual FoxPro が特定のレコードの削除だけをマークすることを指定します。  
  
 *FilterCondition*レコードが削除対象としてマークを満たす必要のある条件を指定します。 AND で接続して、必要な数のフィルター条件を含めることができますか、OR 演算子。 NOT 演算子を使用して、論理式の値を反転するかを使用することができます**空**空のフィールドを確認する ()。  
  
## <a name="remarks"></a>コメント  
 削除設定は、ON に設定されている場合、レコードが削除対象としてマークは、スコープが含まれているすべてのコマンドによって無視されます。  
  
 削除 - 共有アクセス用の複数レコードのテーブルの削除をマークするときに、レコード ロックを開く SQL 使用します。 これにより、マルチ ユーザーの状況でレコードの競合が減少が、パフォーマンスが低下することができます。 最高のパフォーマンスを排他的にテーブルを開きます。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションでは、ODBC SQL ステートメントの削除をデータ ソースに送信するときに、Visual FoxPro ODBC ドライバーを翻訳しないで、Visual FoxPro の削除のコマンドに、コマンドに変換します。  
  
## <a name="see-also"></a>関連項目  
 [SET DELETED コマンド](../../odbc/microsoft/set-deleted-command.md)
