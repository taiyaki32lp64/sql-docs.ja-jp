---
title: Microsoft 拡張機能 SDK for Java
description: Microsoft Extensibility SDK for Java を使用して、SQL Server 用の Java プログラムを実装する方法について説明します。 この SDK は、SQL Server とデータを交換し、SQL Server から Java コードを実行するために使用される Java 言語拡張のインターフェイスです。
ms.prod: sql
ms.technology: language-extensions
ms.date: 11/05/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 66719e8a30b9e7f4e42eaba376c73af9eb9868b2
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658849"
---
# <a name="microsoft-extensibility-sdk-for-java-for-sql-server"></a>SQL Server 用の Microsoft Extensibility SDK for Java
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Microsoft Extensibility SDK for Java を使用して、SQL Server 用の Java プログラムを実装する方法について説明します。 この SDK は、SQL Server とデータを交換し、SQL Server から Java コードを実行するために使用される Java 言語拡張のインターフェイスです。

この SDK は SQL Server 2019 リリース候補 1 の一部として Windows と Linux の両方にインストールされます。

+ Windows の既定のインストール パス: **[instance installation home directory]\MSSQL\Binn\mssql-java-lang-extension.jar**
+ Linux の既定のインストール パス: **/opt/mssql/lib/mssql-java-lang-extension.jar**

このコードはオープンソースであり、[SQL Server 言語拡張の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions)に掲載されています。

## <a name="implementation-requirements"></a>実装の要件

この SDK のインターフェイスには、Java ランタイムと通信するために SQL Server に満たす必要がある一連の要件が定義されています。 この SDK を使用するには、メイン クラスのいくつかの実装ルールに従う必要があります。 SQL Server で Java 言語拡張を使用し、Java クラスの特定のメソッドを実行してデータを交換することができます。

SDK の使用方法の例については、「[チュートリアル:Java で正規表現 (regex) を使用して文字列を検索する](../tutorials/search-for-string-using-regular-expressions-in-java.md)」を参照してください。

## <a name="sdk-classes"></a>SDK のクラス

SDK は、3 つのクラスで構成されています。

SQL Server との間でデータを交換するために Java 拡張機能で使用されるインターフェイスを定義する 2 つの抽象クラス。

- **AbstractSqlServerExtensionExecutor**
- **AbstractSqlServerExtensionDataset**

3 つ目のクラスは、データ セット オブジェクトの実装を含むヘルパー クラスです。 これは、使用できる省略可能なクラスです。利用すると、初めての場合に簡単になります。 代わりに、このようなクラスの独自の実装を使用することもできます。

- **PrimitiveDataset**

次に SDK の各クラスについて説明します。 SDK クラスのソース コードは、[SQL Server 言語拡張の GitHub リポジトリ](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/java/sdk)で入手できます。

### <a name="class-abstractsqlserverextensionexecutor"></a>クラス:AbstractSqlServerExtensionExecutor

抽象クラス **AbstractSqlServerExtensionExecutor** には、SQL Server 用の Java 言語拡張から Java コードを実行するときに使用されるインターフェイスが含まれています。

メイン Java クラスは、このクラスを継承する必要があります。 このクラスから継承するということは、独自のクラスで実装する必要がある特定のメソッドがクラスにあることを意味します。

この抽象クラスから継承するには、クラス宣言で抽象クラス名を使用して拡張します。

```java
public class <MyClass> extends AbstractSqlServerExtensionExecutor {}
```

少なくとも、メイン クラスは execute(...) メソッドを実装する必要があります。

#### <a name="method-execute"></a>メソッド execute

execute メソッドは、SQL Server から Java コードを呼び出すために、Java 言語拡張を介して SQL Server から呼び出されるメソッドです。 これは、SQL Server から実行する主な操作を含める重要なメソッドです。

メソッド引数を SQL Server から Java に渡すには、`sp_execute_external_script` の `@param` パラメーターを使用します。 メソッド **execute** は引数をこの方法で受け取ります。

```java
public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params)  {}
```

#### <a name="method-init"></a>メソッド init

init メソッドは、コンストラクターの後、execute メソッドの前に実行されます。 execute(...) の前に実行する必要がある操作は、このメソッドで実行できます。

```java
public void init(String sessionId, int taskId, int numtask) {}
```

### <a name="class-abstractsqlserverextensiondataset"></a>クラス:AbstractSqlServerExtensionDataset

抽象クラス **AbstractSqlServerExtensionDataset** には、Java 拡張機能で使用される入力データと出力データを処理するためのインターフェイスが含まれています。


### <a name="class-primitivedataset"></a>クラス:PrimitiveDataset

クラス **PrimitiveDataset** は、単純型をプリミティブ配列として格納する **AbstractSqlServerExtensionDataset** の実装です。

この SDK では、単なる省略可能なヘルパー クラスとして提供されています。 このクラスを使用しない場合は、**AbstractSqlServerExtensionDataset** から継承する独自のクラスを実装する必要があります。  

## <a name="next-steps"></a>次の手順

+ [チュートリアル: Java で正規表現 (regex) を使用して文字列を検索する](../tutorials/search-for-string-using-regular-expressions-in-java.md)
+ [SQL Server で Java を呼び出す方法](call-java-from-sql.md)
