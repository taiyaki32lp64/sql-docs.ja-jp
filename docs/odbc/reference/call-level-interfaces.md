---
title: コールレベル インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6c37084ad91a931c4479ecf826c5cb554765412
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135673"
---
# <a name="call-level-interfaces"></a>コールレベル インターフェイス
コールレベル インターフェイス (CLI) は、DBMS に SQL ステートメントを送信するための最終的な手法します。 コールレベル インターフェイスは、アプリケーション プログラムによって呼び出すことができる DBMS 関数のライブラリを提供します。 したがって、別のプログラミング言語と SQL をブレンドするのではなく呼び出しレベルのインターフェイスはプログラマのほとんどが文字列、I/O、または C. 注 embedded SQL をサポートするその Dbms での数値演算ライブラリなど、使用に慣れているが、日常的なライブラリに似ています呼び出し、プリコンパイラによって生成された、呼び出しレベルのインターフェイスが既にあります。 ただし、これらの呼び出しは、ドキュメント化されていない、予告なく変更される可能性が。  
  
 コールレベル インターフェイスは、クライアント/サーバー アーキテクチャ、アプリケーション プログラム (クライアント) が 1 台のコンピューター上に存在し、別のコンピューター上の DBMS (サーバー) でよく使用されます。 アプリケーションがローカルのシステムで CLI 関数を呼び出すし、処理のため、DBMS にこれらの呼び出しをネットワーク経由で送信されます。  
  
 SQL ステートメントは、実行時に処理するため、DBMS に渡されるとは異なり、埋め込み SQL 全体として組み込みの SQL ステートメントがないと、プリコンパイル済みの必要はありませんが、呼び出しレベルのインターフェイスが動的 SQL に似ています。  
  
 通常の呼び出しレベルのインターフェイスを使用するには、次の手順が含まれます。  
  
1.  アプリケーションでは、DBMS に接続するための CLI 関数を呼び出します。  
  
2.  アプリケーションでは、SQL ステートメントを構築し、バッファーに配置されます。 これは、後、ステートメントの準備と実行の DBMS を送信する 1 つ以上の CLI 関数を呼び出します。  
  
3.  ステートメントが SELECT ステートメントの場合は、アプリケーションはアプリケーション バッファーで、結果を返すことの CLI 関数を呼び出します。 通常、この関数を返します 1 行または 1 つの列のデータを時に。  
  
4.  アプリケーションでは、DBMS から切断する CLI 関数を呼び出します。
