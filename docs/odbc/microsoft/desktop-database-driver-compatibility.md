---
title: デスクトップ データベース ドライバーの互換性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31263162526b6bd2e0a116a473f09f9e2caeba94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077283"
---
# <a name="desktop-database-driver-compatibility"></a>デスクトップ データベース ドライバーの互換性
Unicode は、ソフトウェア文字エン コードのメソッドのすべての文字を 2 バイトの固定幅を持つものとして扱われます。 このメソッドは、1 バイト文字を表すためには、256 文字に限定されている Windows の ANSI 文字のエンコード、代替手段として使用されます。 文字は表されない多数の言語に対応 Unicode が 65,000 を超える文字を表すことのできるため、ANSI エンコーディングにします。  
  
 ODBC 3.5 (またはそれ以降) のドライバー マネージャーは、Unicode に対応します。 これは 2 つの主要な領域に影響します。 関数呼び出しと、文字列データ型。 ドライバー マネージャー マップ関数の文字列引数と文字列データはアプリケーションおよびドライバーによって必要に応じては Unicode 対応または ANSI 対応のいずれかをどちらもできます。  
  
 ODBC 3.5 (またはそれ以降) のドライバー マネージャーでは、Unicode アプリケーションと、ANSI アプリケーションの両方で Unicode ドライバーの使用をサポートします。 また、ANSI アプリケーションに、ANSI ドライバーの使用もサポートしています。 ドライバー マネージャーは、Unicode アプリケーションの場合、ANSI ドライバー操作の制限付きの Unicode から ANSI マッピングを提供します。 これにより、Jet の 3.5 データベースとすべての既存 ISAM ファイルの種類のサポートを利用できます。  
  
 ANSI アプリケーションが ODBC デスクトップ データベース ドライバー 4.0 を使用し、Microsoft Access 4.0 にアクセスするまたは後で、ドライバーとして公開するデータ型 SQL_CHAR、sql_varchar、SQL_LONGVARCHAR Jet 4.0 には、ワイド バージョンがサポートされています。 以前のバージョンの Jet では、SQL_WCHAR、SQL_WVARCHAR、SQL_WLONGVARCHAR は使用できません。 この制限は、Jet 4.0 データベース エンジンの以前の書式設定が使用されている場合にも適用されます。  
  
 ODBC での Unicode の問題に関する詳細については、次を参照してください。 [Unicode](../../odbc/reference/develop-app/unicode.md)プログラミングの考慮事項。
