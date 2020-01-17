---
title: Unicode |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e0044a2e2efbf0d8921a07ed4679806ba50bcd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087562"
---
# <a name="unicode"></a>Unicode
Unicode では、多くの言語での文字のエンコードを定義します。  
  
 Unicode 規格の詳細については、次を参照してください。 [、Unicode Consortium](https://www.unicode.org)します。  
  
 Unicode では、ユニバーサル文字セットを定義します。 Windows の ANSI コード ページは、通常 1 つの言語の文字を含む、文字セットを定義します。 異なるコード ページを使用するために必要なアプリケーションを記述するより難しい場合があります。  
  
 Unicode では、コード ページは必要ありません。 すべてのコード ポイントは、いくつかの言語で 1 つの文字にマップされます。  
  
 現在唯一の Unicode エンコーディングの ODBC をサポートしているは、ucs-2 は、の文字を表す 16 ビット整数 (固定長) を使用します。 Unicode では、さまざまな言語で動作するアプリケーションができます。  
  
 ODBC 3.5 (またはそれ以降) のドライバー マネージャーは、Unicode に対応します。 これは 2 つの主要な領域に影響します。 関数呼び出しと、文字列データ型。 ドライバー マネージャー マップ関数の文字列引数と文字列データはアプリケーションおよびドライバーによって必要に応じては Unicode 対応または ANSI 対応のいずれかをどちらもできます。 これら 2 つの領域が、セクションで詳しく説明されている[Unicode 関数の引数](../../../odbc/reference/develop-app/unicode-function-arguments.md)と[Unicode データ](../../../odbc/reference/develop-app/unicode-data.md)します。  
  
 ODBC 3.5 (またはそれ以降) のドライバー マネージャーでは、Unicode アプリケーションと、ANSI アプリケーションの両方で Unicode ドライバーの使用をサポートします。 また、ANSI アプリケーションに、ANSI ドライバーの使用もサポートしています。 ドライバー マネージャーは、Unicode アプリケーションの場合、ANSI ドライバー操作の制限付きの Unicode から ANSI マッピングを提供します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Unicode 関数の引数](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode データ](../../../odbc/reference/develop-app/unicode-data.md)
