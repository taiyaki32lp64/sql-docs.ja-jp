---
title: テキストとイメージの列の管理 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a161b009239db3c17acb64f8d8eeaaa61321cd9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63195318"
---
# <a name="managing-text-and-image-columns"></a>text 列と image 列の管理
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **テキスト**、 **ntext**、および**イメージ**データ (長い形式のデータとも呼ばれる) は文字またはバイナリ文字列データ型に収まるようには大きすぎるデータ値を保持できる**char**、 **varchar**、**バイナリ**、または**varbinary**列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **テキスト**データ型は ODBC SQL_LONGVARCHAR データ型にマップされます**ntext** sql_wlongvarchar と**イメージ**にマップされます。 長いドキュメントや大きなビットマップなど、データ アイテムの中には大きすぎて適切にメモリに読み込むことができないものもあります。 長いデータを取得する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]シーケンシャルの部分で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーにより、アプリケーションを呼び出す[SQLGetData](../native-client-odbc-api/sqlgetdata.md)します。 シーケンシャルな部分で長い形式のデータを送信するアプリケーションを呼び出すことができます[SQLPutData](../native-client-odbc-api/sqlputdata.md)します。 実行時にデータ送信に使われるパラメーターを、実行時データ パラメーターと呼びます。  
  
 アプリケーションが実際に作成またはであらゆる種類のデータ (データの間だけ) を取得**SQLPutData**または**SQLGetData**だけですが、**文字**と**バイナリ**データを送信または部分で取得できます。 ただし、データが 1 つのバッファーに合わせて大きさの場合は、理由はありません一般的に使用する**SQLPutData**または**SQLGetData**します。 バッファーをパラメーターまたは列にバインドする方がはるかに簡単です。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [バインドされた text、image 型の列とバインドされない text、image 型の列](bound-vs-unbound-text-and-image-columns.md)  
  
-   [ログに記録される変更と記録されない変更](logged-vs-unlogged-modifications.md)  
  
-   [実行時データと Text 型、ntext 型、または Image 型の列](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
