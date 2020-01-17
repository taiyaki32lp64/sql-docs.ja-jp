---
title: 位置指定更新と Delete ステートメントのシミュレート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85d7642620d510ebba050a3fbc4348898e070070
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107531"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>位置指定の UPDATE および DELETE ステートメントのシミュレート
データ ソースの位置指定更新をサポートおよび delete ステートメントがないの場合、ドライバーはこれらをシミュレートできます。 たとえば、ODBC カーソル ライブラリでは、位置指定更新をシミュレートし、ステートメントを削除します。 位置指定更新と delete ステートメントをシミュレートするための一般的な戦略では、位置指定のステートメントを検索したものに変換します。 置き換えることで、これは、 **WHERE CURRENT OF** 、検索結果を含む**WHERE**句現在の行を識別する句。  
  
 たとえば、CustID 列は、Customers テーブルの各行を一意に識別する、ため、位置指定削除ステートメント  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 変換する場合があります。  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 ドライバーは、次のいずれかを使用して可能性があります*行識別子*で、**WHERE**句。  
  
-   列の値を持つテーブルのすべての行に一意に識別するためにサービスを提供します。 たとえば、呼び出し**SQLSpecialColumns** SQL_BEST_ROWID、最適な列または列をこの目的のセットを返します。  
  
-   すべての行を一意に識別するために、一部のデータ ソースによって提供される擬似列。 これらもあります取得可能呼び出して**SQLSpecialColumns**します。  
  
-   使用可能な場合は一意なインデックス、します。  
  
-   結果セットのすべての列です。  
  
 のどの列だけでドライバーを使用する必要があります、**WHERE**構築句は、ドライバーによって異なります。 一部のデータで行識別子を決定する、ソースがコストのかかるできます。 ただし、高速化は、実行して、シミュレートされたステートメントを更新または最大で 1 行を削除ことが保証されます。 基になる DBMS の機能によっては、行識別子を使用してセットアップにかかるコストがあります。 ただし、高速化は、実行して、シミュレートされたステートメントは更新または 1 行のみを削除することが保証されます。 結果セット内のすべての列を使用して、オプションは、セットアップをはるかに簡単です。 ただし、実行に時間がかかりますが、列は行を一意に識別されないため、誤って更新または削除される行で発生することができる場合、結果の select リストが設定した場合に特には、基になるテーブルに存在するすべての列。  
  
 サポートによって、上記の方法のうち、ドライバー、アプリケーション SQL_ATTR_SIMULATE_CURSOR ステートメント属性を使用するドライバーがどの方法を選択することができます。 アプリケーションのリスクの意図を更新または行を削除するのには奇数ように見えますが、アプリケーションは、結果セット内の列は、結果セット内の各行を一意に識別できるようにしてこのリスクを削除できます。 これは、ドライバーに、これを行う手間を保存します。  
  
 インターセプト行識別子を使用する場合、ドライバー、 **SELECT FOR UPDATE**結果セットを作成するステートメント。 選択リスト内の列は行を効率的に識別しない場合、ドライバーは、選択リストの末尾に必要な列を追加します。 一部のデータ ソースが oracle; ROWID 列などの行を常に一意に識別する 1 つの列があります。このような列を使用できる場合、ドライバーはこれを使用します。 それ以外の場合、ドライバーを呼び出す**SQLSpecialColumns**の各テーブルに対して、 **FROM**各行を一意に識別する列の一覧を取得する句。 この方法に起因する一般的な制限は、カーソルのシミュレーションは失敗で 1 つ以上のテーブルがある場合、 **FROM**句。  
  
 削除には、通常のドライバーが行を特定する方法に関係なく、 **FOR UPDATE OF**オフ句、 **SELECT FOR UPDATE**データ ソースに送信する前にステートメント。 **FOR UPDATE OF**句が優位性を update および delete ステートメントのみに使用されます。 サポートしないデータ ソースには、更新プログラムが配置されているし、delete ステートメントの通常ではサポートされません。  
  
 アプリケーションでは、位置指定の update または delete ステートメントの実行を送信すると、ドライバーによって置き換えられます、 **WHERE CURRENT OF**句、**WHERE**句を含む行の識別子。 これらの列の値を使用して、各列用のドライバーによって保持されるキャッシュから取得されます、**WHERE**句。 ドライバーを表示した後、**WHERE**句では、送信、ステートメントの実行のデータ ソースをします。  
  
 たとえば、アプリケーションが結果セットを作成する次のステートメントを送信します。  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 アプリケーションが要求の一意性を保証する SQL_ATTR_SIMULATE_CURSOR を設定し、データ ソースが行を常に一意に識別する擬似列を提供していない場合、ドライバーを呼び出す場合**SQLSpecialColumns**用、Customers テーブルは CustID の Customers テーブルにキーがして、選択のリストに追加してを除去ことを検出します。、 **FOR UPDATE OF**句。  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 アプリケーションが一意性を保証、要求されていない場合、ドライバーを除去のみ、 **FOR UPDATE OF**句。  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Cust が結果セットに対して、カーソルの名前をアプリケーションが結果セットをスクロールし、実行するための次の位置指定の update ステートメントを送信するとします。  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 アプリケーションが、一意性を保証を要求していない、ドライバーに置き換わります、**WHERE**句 CustID パラメーターをキャッシュ内の変数にバインドします。  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 アプリケーションが、一意性を保証を要求していない、ドライバーに置き換わります、**WHERE**句およびそのキャッシュ内の変数にこの句で名前、アドレス、および電話のパラメーターをバインドします。  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
