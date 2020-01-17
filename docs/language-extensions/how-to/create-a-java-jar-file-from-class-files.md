---
title: クラス ファイルから Java jar ファイルを作成する
description: クラス ファイルから Java jar ファイルを作成する方法について説明します。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5a53eb4b8da04a799461dcb1e0cb32feff2fe6f
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658867"
---
# <a name="create-a-java-jar-file-from-class-files"></a>クラス ファイルから Java jar ファイルを作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[SQL Server 言語拡張](../language-extensions-overview.md)を使用して Java コードを実行するとき、クラス ファイルを jar ファイルにパッケージ化する方法について説明します。 ファイルをパッケージ化することをお勧めします。

## <a name="create-a-jar-file"></a>jar ファイルを作成する

クラス ファイルから jar を作成するには、クラス ファイルが格納されているフォルダーに移動し、次のコマンドを実行します。

```cmd
jar -cf <MyJar.jar> *.class
```

`jar.exe` のパスがシステム パス変数の一部であることを確認します。 または、JDK フォルダーの `/bin` 以下にある jar の完全なパスを指定します。 例:

```cmd
C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class
```

## <a name="next-steps"></a>次の手順

+ [SQL Server 言語拡張で Java ランタイムを呼び出す方法](../how-to/call-java-from-sql.md)