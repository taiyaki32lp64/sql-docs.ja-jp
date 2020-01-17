---
title: 分離レベルについて |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2c41e23a-da6c-4650-b5fc-b5fe53ba65c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b4886b1bd0f4ff62df06334af469a76b64600839
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027392"
---
# <a name="understanding-isolation-levels"></a>分離レベルについて

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

各トランザクションでは、別のトランザクションによって行われたリソースまたはデータの変更から特定のトランザクションを分離する際の程度を定義する分離レベルを指定します。 分離レベルは、ダーティ リードやファントム読み取りなど、コンカレンシーの副作用を許可するかどうかという観点で定義されています。  
  
トランザクション分離レベルでは次の制御を行います。  
  
- データの読み取り時にロックを獲得するかどうか、要求されるロックの種類。  
  
- 読み取りロックの保持期間。  
  
- 別のトランザクションによって変更された行を参照している読み取り操作で、次のことを行うかどうか。  
  
  - その行に対する排他ロックが解放されるまでブロックする。  
  
  - ステートメントまたはトランザクションの開始時に存在していた行の、コミット済みのバージョンを取得する。  
  
  - コミットされていないデータ変更を読み取る。  

トランザクション分離レベルを選択しても、データ変更を保護するために獲得したロックは影響を受けません。 トランザクションでは、設定されたトランザクション分離レベルに関係なく、常に、そのトランザクションで変更するデータについて排他ロックを獲得し、トランザクションが完了するまでそのロックを保持します。 トランザクション分離レベルでは主に、読み取り操作に対して、他のトランザクションによって行われる変更の影響からの保護レベルを定義します。  
  
分離レベルが低いほど多くのユーザーが同時にデータにアクセスできるようになりますが、ユーザーに影響が及ぶ可能性があるコンカレンシーの影響 (ダーティ リードや更新データの喪失など) の種類が多くなります。 反対に、分離レベルが高いほど、ユーザーに影響が及ぶ可能性があるコンカレンシーの影響の種類は減りますが、必要なシステム リソースが増加し、あるトランザクションによって別のトランザクションがブロックされる状況も多くなります。 適切な分離レベルの選択は、アプリケーションのデータ整合性の要件と各分離レベルのオーバーヘッドとのバランスによって決まります。 最も高い分離レベルの SERIALIZABLE は、トランザクションで読み取り操作が繰り返し実行されるたびに、そのトランザクションで完全に同じデータが取得されることを保証します。このことの実現には、マルチユーザー システムにおいて他のユーザーが影響を受ける可能性が高いロック レベルが適用されています。 最も低い分離レベルは READ UNCOMMITTED ですが、このレベルでは、他のトランザクションによって変更され、まだコミットされていないデータを取得する場合があります。 コンカレンシーのあらゆる副作用が READ UNCOMMITTED では生じる可能性がありますが、読み取りロックやバージョニングは発生しないため、オーバーヘッドはごくわずかです。  

## <a name="remarks"></a>Remarks

 次の表は、分離レベルごとのコンカレンシーの副作用を示しています。  
  
| [分離レベル]  | ダーティ リード | 反復不能読み取り | ファントム |
| ---------------- | ---------- | ------------------- | ------- |
| READ UNCOMMITTED | はい        | はい                 | はい     |
| READ COMMITTED   | いいえ         | はい                 | はい     |
| REPEATABLE READ  | いいえ         | いいえ                  | はい     |
| スナップショット         | いいえ         | いいえ                  | いいえ      |
| Serializable     | いいえ         | いいえ                  | いいえ      |
  
2 つのトランザクションが同じ行を取得すると、更新内容の喪失が生じる可能性がありますが、この状況を防ぐためには、REPEATABLE READ 以上の分離レベルでトランザクションを実行し、その後で、元の取得した値に基づいて行を更新する必要があります。 2 つのトランザクションが、元の取得した値に基づかずに 1 つの UPDATE ステートメントを使用して行を更新する場合、既定の分離レベル READ COMMITTED では更新データの喪失が発生しません。  

トランザクションの分離レベルを設定するには、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [setTransactionIsolation](../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md) メソッドを使用できます。 このメソッドは、引数として **int** 値を受け取ります。この値は、次のように接続定数のいずれかに基づいています。  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);  
```

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいスナップショット分離レベルを使用するには、`SQLServerConnection` 定数のいずれかを使用できます。  

```java
con.setTransactionIsolation(SQLServerConnection.TRANSACTION_SNAPSHOT);  
```

また、次のように使用することもできます。  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED + 4094);  
```

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の分離レベルの詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[!INCLUDE[ssDE](../../includes/ssde_md.md)]における分離レベル」を参照してください。  

## <a name="see-also"></a>参照

[JDBC ドライバーを使用したトランザクションの実行](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
