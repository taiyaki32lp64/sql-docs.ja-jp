---
title: ODBC データソースサブキー |Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d6d54d1fc7c7742bf94e91d7370f356e28b5624
ms.sourcegitcommit: 816ff47eeab157c66e0f75f18897a63dc8033502
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71207688"
---
# <a name="odbc-data-sources-subkey"></a>ODBC データソースサブキー

サブキーの`ODBC Data Sources`下の値には、データソースが一覧表示されます。 これらの値の形式を次の表に示します。

| 名前 | データ型 | data |
| :--- | :-------- | :--- |
| *data-source-name* | REG_SZ | *ドライバー-説明* |
| &nbsp; | &nbsp; | &nbsp; |

*データソース名*の値は、管理プログラムによって定義されます (通常はユーザーにプロンプトを表示します)。*ドライバーの説明*は、ドライバーの開発者によって定義されます (通常は、ドライバーに関連付けられている DBMS の名前です)。

たとえば、3つのデータソースが定義されているとします。インベントリ。 SQL Server を使用します。DBASE を使用する Payroll書式設定されたテキストファイルを使用するスタッフ。 サブキーの`ODBC Data Sources`下の値は次のようになります。

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
