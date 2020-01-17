---
title: データ ソースのファイル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d27f168640b25652ed0fd40154ebfb677ef9300
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068646"
---
# <a name="file-data-sources"></a>[ファイル データ ソース]
*データ ソースをファイル*はファイルに格納され、1 人のユーザーによって繰り返し使用することもいくつかのユーザー間で共有への接続情報を許可します。 ファイル データ ソースを使用すると、ドライバー マネージャーは .dsn ファイルに情報を使用してデータ ソースへの接続を使用します。 このファイルは、その他のファイルのように操作できます。 ファイル データ ソースをは、コンピューターのデータ ソースを行い、任意の 1 人のユーザーまたはコンピューターに登録されていないと、データ ソース名がありません。  
  
 ファイル データ ソースを .dsn ファイルには、呼び出し用にビルドする必要がありますそれ以外の場合、接続文字列が含まれているため、接続プロセスを効率化、 **SQLDriverConnect**関数。 .Dsn ファイルのもう 1 つの利点をコピーできます任意のコンピューターにインストールされている適切なドライバーがある限り、同一のデータ ソースは多くのマシンで使用できるようにします。 ファイルのデータ ソースは、アプリケーションでも共有できます。 ファイルの共有データ ソースをネットワーク上に配置し、複数のアプリケーションで同時に使用します。  
  
 .Dsn ファイルが共有可能なことができますもあります。 共有不能な .dsn ファイルは、1 台のコンピューター上に存在し、コンピューターのデータ ソースを指します。 共有不能なファイル データ ソースは、ファイル データ ソースのみを使用するアプリケーションを設計できるように、マシンのデータ ソースのファイル データ ソースへの簡単な変換を許可するには、主に存在します。 ドライバー マネージャーは、共有不能なファイルのデータ ソースの情報を送信するときを .dsn ファイルを指すコンピューターのデータ ソースに接続します。  
  
 ファイル データ ソースの詳細については、次を参照してください。[を使用してファイル データ ソースの接続](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)、または[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)関数の説明。
