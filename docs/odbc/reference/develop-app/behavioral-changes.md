---
title: 動作の変更 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fc9f8dcc3782204c8bf1c9add1200e451edcf127
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103875"
---
# <a name="behavioral-changes"></a>動作の変更
動作の変更はそれらの変更を*構文*は同じインターフェイスが、*セマンティクス*が変更されました。 この変更では、ODBC 2 で使用される機能です。*x* ODBC 3 で同じ機能の動作は異なります *。x*します。  
  
 かどうかをアプリケーションには、ODBC 2 が発生します。*x*動作または ODBC 3 *。x* SQL_ATTR_ODBC_VERSION [環境] 属性で動作が決まります。 この 32 ビット値は、ODBC 2 が発生する SQL_OV_ODBC2 に設定されます。*x*動作、および ODBC 3 が発生する SQL_OV_ODBC3 *。x*動作します。  
  
 呼び出して SQL_ATTR_ODBC_VERSION 環境属性が設定**SQLSetEnvAttr**します。 アプリケーションから**SQLAllocHandle**環境ハンドルを割り当てるを呼び出す必要があります**SQLSetEnvAttr**従来の動作を設定するには、すぐにします。 (その結果は、新しい環境の状態、割り当て済みで、versionless、環境ハンドルを記述する状態)。詳細については、次を参照してください[付録 b:。ODBC の状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)します。  
  
 アプリケーションでは、従来の SQL_ATTR_ODBC_VERSION 環境属性が属性にどのような動作は、ODBC 2 とアプリケーションの接続に影響を与えませんを示しています。*x*または ODBC 3 *。x*ドライバー。 ODBC 3。*x*アプリケーションに、ODBC 2 との接続のことができます *。x*または 3 *。x*環境の属性の設定に関係なく、ドライバー。  
  
 ODBC 3。*x*アプリケーションは呼び出さないで**SQLAllocEnv**します。 ドライバー マネージャーへの呼び出しを受信した場合、結果として**SQLAllocEnv**、ODBC 2 としてアプリケーションを認識します *。x*アプリケーション。  
  
 SQL_ATTR_ODBC_VERSION 属性は、ODBC 3 の 3 つのさまざまな側面に影響します。*x*ドライバーの動作。  
  
-   SQLSTATE  
  
-   日付、時刻、およびタイムスタンプのデータ型  
  
-   *CatalogName*引数**SQLTables** ODBC 3 内の検索パターンを受け入れます *。x*、ODBC 2 ではなく *。x*  
  
 SQL_ATTR_ODBC_VERSION 環境属性の設定には影響しません**SQLSetParam**または**SQLBindParam**します。 **SQLColAttribute**も受けませんこのビット。 **SQLColAttribute**影響を受ける属性を返します (日付型、有効桁数、小数点、および長さ)、ODBC のバージョンで、目的の動作がの値によって決まりますが、 *FieldIdentifier*引数。 ときに*FieldIdentifier* SQL_DESC_TYPE、等しく**SQLColAttribute** ODBC 3 が返されます *。x*日付、時刻、およびタイムスタンプのコードと*FieldIdentifier* SQL_COLUMN_TYPE、等しく**SQLColAttribute** ODBC 2 を返します *。x*日付、時刻、およびタイムスタンプのコード。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQLSTATE マッピング](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [datetime データ型の変更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
