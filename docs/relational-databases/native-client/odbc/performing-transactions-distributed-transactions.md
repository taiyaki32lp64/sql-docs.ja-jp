---
title: 分散トランザクションを作成する |Microsoft Docs
ms.custom: ''
ms.date: 05/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b01e47f81f153b73c8a57d23c9a75fc8b57ef66
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761072"
---
# <a name="create-a-distributed-transaction"></a>分散トランザクションの作成

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


分散トランザクションは、さまざまな方法でさまざまな Microsoft SQL システムに対して作成できます。

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>ODBC ドライバーは SQL Server オンプレミスの MSDTC を呼び出します。

Microsoft 分散トランザクションコーディネーター (MSDTC) を使用すると、アプリケーションは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の2つ以上のインスタンスにわたってトランザクションを拡張または_配信_できます。 分散トランザクションは、2つのインスタンスが別々のコンピューターでホストされている場合でも機能します。

MSDTC はオンプレミス Microsoft SQL Server 用にインストールされていますが、Microsoft の Azure SQL Database クラウドサービスでは使用できません。

MSDTC は、 C++プログラムが分散トランザクションを管理するときに、SQL Server Native Client driver for OPEN DATABASE CONNECTIVITY (ODBC) によって呼び出されます。 Native Client ODBC ドライバーには、Open Group Distributed Transaction Processing (DTP) XA 標準に準拠しているトランザクションマネージャーがあります。 このコンプライアンスは MSDTC によって要求されます。 通常、すべてのトランザクション管理コマンドは、この Native Client ODBC ドライバーを介して送信されます。 シーケンスは次のとおりです。

1. C++ NATIVE Client ODBC アプリケーションでは、自動コミットモードがオフになっている状態で[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)を呼び出すことによってトランザクションを開始します。

2. アプリケーションは、コンピューター A 上の SQL Server X の一部のデータを更新します。

3. アプリケーションは、コンピューター B 上の SQL Server Y の一部のデータを更新します。
    - SQL Server Y で更新が失敗した場合、両方の SQL Server インスタンスのすべてのコミットされていない更新がロールバックされます。

4. 最後に、SQL_COMMIT または SQL_ROLLBACK オプションを使用して、 [SQLEndTran _(1)_ ](../../../relational-databases/native-client-odbc-api/sqlendtran.md)を呼び出すことによってトランザクションを終了します。

_(1)_ ODBC を使用せずに MSDTC を呼び出すことができます。 このような場合、MSDTC はトランザクションマネージャーになり、アプリケーションは**SQLEndTran**を使用しなくなります。

### <a name="only-one-distributed-transaction"></a>1つの分散トランザクションのみ

C++ NATIVE Client ODBC アプリケーションが分散トランザクションに参加しているとします。 次に、アプリケーションが2番目の分散トランザクションに参加します。 この場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは元の分散トランザクションを残し、新しい分散トランザクションに参加します。

詳細については、「 [DTC プログラマーズリファレンス](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\))」を参照してください。

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C#クラウドでの SQL Database の代替手段

Azure SQL Database または Azure SQL Data Warehouse で MSDTC はサポートされていません。

ただし、 C#プログラムで .net クラスの[TransactionScope](/dotnet/api/system.transactions.transactionscope)を使用することによって、SQL Database に対して分散トランザクションを作成できます。

### <a name="other-programming-languages"></a>その他のプログラミング言語

次の他のプログラミング言語では、SQL Database サービスを使用した分散トランザクションのサポートが提供されない場合があります。

- ODBC C++ドライバーを使用するネイティブ
- Transact-sql を使用したリンクサーバー
- JDBC ドライバー

## <a name="see-also"></a>参照

[トランザクションの実行 (ODBC)](performing-transactions-in-odbc.md)
