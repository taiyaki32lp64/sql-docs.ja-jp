---
title: Text 列と Image 列の管理 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 221d83188a3d48fe5383a109b878c7b5a59bdad5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73758396"
---
# <a name="managing-text-and-image-columns"></a>text 列と image 列の管理
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **text**、 **ntext**、および**image**データ (長い形式のデータとも呼ばれる) は文字またはバイナリ文字列データ型に収まるようには大きすぎるデータ値を保持できる**char**、 **varchar**、**binary**、または**varbinary**列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **text**データ型は ODBC SQL_LONGVARCHAR データ型にマップされます**ntext** sql_wlongvarchar と**image**にマップされます。 長いドキュメントや大きなビットマップなど、データ アイテムの中には大きすぎて適切にメモリに読み込むことができないものもあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から長いデータを連続して取得するために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを使用すると、アプリケーションは[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)を呼び出すことができます。 長いデータをシーケンシャルな部分に送信するために、アプリケーションは[Sqlputdata](../../relational-databases/native-client-odbc-api/sqlputdata.md)を呼び出すことができます。 実行時にデータ送信に使われるパラメーターを、実行時データ パラメーターと呼びます。  
  
 アプリケーションが実際に作成またはであらゆる種類のデータ (データの間だけ) を取得**SQLPutData**または**SQLGetData**だけですが、**character**と**binary**データを送信または部分で取得できます。 ただし、データが1つのバッファーに収まらない場合は、通常、 **Sqlputdata**または**SQLGetData**を使用する必要はありません。 バッファーをパラメーターまたは列にバインドする方がはるかに簡単です。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [バインドされたテキストと画像の列](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [ログに記録された変更と Unlogged の変更](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [実行時データと Text 型、ntext 型、または Image 型の列](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
