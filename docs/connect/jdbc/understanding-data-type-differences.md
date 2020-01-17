---
title: データ型の違いについて |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 906a4abf0768fcad2e5ac31a0ee93345dcc8b30c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027380"
---
# <a name="understanding-data-type-differences"></a>データ型の違いについて

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Java プログラミング言語のデータ型と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型には、異なる点が多数あります。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、さまざまな型の変換を行うことによって、これらの違いに対応しています。  

## <a name="character-types"></a>文字型

JDBC 文字列のデータ型は**CHAR**、 **VARCHAR**、および**longvarchar**です。 JDBC ドライバーでは、JDBC 4.0 API がサポートされます。 JDBC 4.0 では、JDBC 文字列のデータ型も**NCHAR**、 **NVARCHAR**、および**LONGNVARCHAR**にすることができます。 これらの新しい文字列型では Java のネイティブの文字型が Unicode 形式で維持されるため、ANSI から Unicode への変換または Unicode から ANSI への変換を実行する必要がありません。  
  
| 型            | [説明]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 固定長    | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Char**および**nchar**データ型は、JDBC **char**および**nchar**型に直接マップされます。 列が `SET ANSI_PADDING ON` の場合、このサーバーが埋め込みを行う固定長の型です。 埋め込みは **nchar** に対しては常にオンですが、**char** に対しては、サーバーにより char 列の埋め込みが行われていない場合は、JDBC ドライバーが埋め込みを行います。                                                                                                                                                                                                                                                                                                                                                                                      |
| 可変長 | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Varchar**型と**nvarchar**型は、それぞれ JDBC **varchar**型と**nvarchar**型に直接マップされます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Long            | **Text** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]型と**ntext**型は、それぞれ JDBC **longvarchar**と**LONGNVARCHAR**型にマップされます。 これらは、以降では[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]非推奨の型なので、大きな値の型 **(varchar (max)** または**nvarchar (max))** を使用する必要があります。<br /><br /> Update\<数値型 > および[updateobject (int, java)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md)メソッドを使用すると、 **text**列と**ntext**サーバー列に対して失敗します。 ただし、サーバーの **text** 列と **ntext** 列に対して、文字変換の型を指定して [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) メソッドを使用することは可能です。 |
  
## <a name="binary-string-types"></a>バイナリ文字列型

JDBC バイナリ文字列型は、 **binary**、 **VARBINARY**、および**longvarbinary**です。  
  
| 型            | [説明]                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 固定長    | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **バイナリ**型は、JDBC**バイナリ**型に直接マップされます。 列が SET ANSI_PADDING ON の場合、これはサーバーが埋め込みを行う固定長の型です。 サーバーの char 列に埋め込みが行われていない場合は、JDBC ドライバーが埋め込みを行います。<br /><br /> タイムスタンプ型は、8バイトの固定長を持つ JDBC**バイナリ**型です。 **** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |
| 可変長 | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Varbinary**型は、JDBC **varbinary**型にマップされます。<br /><br /> の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **udt** 型は、 **VARBINARY**型として JDBC にマップされます。                                                                                                                                                                                                                                 |
| Long            | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **イメージ**の種類は、JDBC **longvarbinary**型にマップされます。 この型は [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降では非推奨とされるため、代わりに大きな値の型である **varbinary(max)** を使用する必要があります。                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>真数型

JDBC の真数型は、対応する SQL Server 型に直接マップされます。  
  
| 型     | [説明]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | JDBC の **BIT** 型は、0 または 1 の単一ビットを表します。 これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ビット**型にマップされます。                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | JDBC の **TINYINT** 型は、1 バイトを表します。 これは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint**型にマップされます。                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | JDBC の **SMALLINT** 型は、符号付きの 16 ビット整数を表します。 これは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint**型にマップされます。                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | JDBC の **INTEGER** 型は、符号付きの 32 ビット整数を表します。 これは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**型にマップされます。                                                                                                                                                                                                                                                                                                                                           |
| bigint   | JDBC の **BIGINT** 型は、符号付きの 64 ビット整数を表します。 これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint**型にマップされます。                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | JDBC の **NUMERIC** 型は、同一有効桁数の値を保持する固定長の有効桁数の 10 進値を表します。 **数値** 型は**数値**型に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]マップされます。                                                                                                                                                                                                                                                                   |
| DECIMAL  | JDBC の **DECIMAL** 型は、指定された有効桁数以上の値を保持する固定長の有効桁数の 10 進値を表します。 **Decimal**型は**10 進数**型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にマップされます。<br /><br /> JDBC の **DECIMAL** 型は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **money** 型と **smallmoney** 型にもマップされます。これらはそれぞれ、8 バイトと 4 バイトで格納される固定長の有効桁数の decimal 型です。 |
  
## <a name="approximate-numeric-types"></a>概数型

JDBC の概数型は、**実数**、 **DOUBLE**、および**FLOAT**です。  
  
| 型   | [説明]                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | JDBC の **REAL** 型の有効桁数は 7 桁 (単精度) で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **real** 型に直接マップされます。                                                                                                                                     |
| DOUBLE | JDBC の **DOUBLE** 型の有効桁数は 15 桁 (倍精度) で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **float** 型にマップされます。 JDBC **FLOAT**型は、 **DOUBLE**のシノニムです。 **FLOAT**と**double**の間には混乱が生じる可能性があるため、 **double**を使用することをお勧めします。 |
  
## <a name="datetime-types"></a>Datetime 型

JDBC**タイムスタンプ**型は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**型と**smalldatetime**型にマップされます。 **datetime** 型は、2 つの 4 バイト整数に格納されます。 **smalldatetime** 型は同じ情報 (日付と時刻) を保持しますが、精度が低く、2 つの 2 バイトの小整数に格納されます。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **timestamp** 型は、固定長のバイナリ文字列型です。 JDBC の時刻型 ( **DATE**、 **time**、 **TIMESTAMP**) のいずれにもマップされません。  
  
## <a name="custom-type-mapping"></a>カスタム型のマッピング

Jdbc の高度な型 (Udt、構造体など) の SQLData インターフェイスを使用する、JDBC のカスタム型マッピング機能。 は、JDBC ドライバーでは実装されていません。  
  
## <a name="see-also"></a>参照

[JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
