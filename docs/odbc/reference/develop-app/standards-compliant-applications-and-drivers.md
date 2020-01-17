---
title: 標準に準拠したアプリケーションとドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4980cfe64a5a8e8404c6b5b0bdc8b1aba484f0c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107331"
---
# <a name="standards-compliant-applications-and-drivers"></a>標準に準拠したアプリケーションとドライバー
標準に準拠したアプリケーションまたはドライバーを開いてグループ CAE 仕様に準拠している 1 つは、"データ管理。SQL 呼び出しレベルのインターフェイス (CLI)、"と ISO/IEC 9075-3:1995 (E) コールレベル インターフェイス (SQL/CLI)。  
  
 ODBC *3.x*で、次の機能が保証されます。  
  
-   Open Group および ISO CLI 仕様に記述されたアプリケーションは、ODBC *3.x*ドライバーまたは ODBC でコンパイルされるときに、標準に準拠したドライバー *3.x*ヘッダー ファイルし、リンクされています。ODBC *3.x*ライブラリ、ドライバーは ODBC へのアクセスを得る場合と*3.x*ドライバー マネージャー。  
  
-   Open Group および ISO CLI 仕様に記述されたドライバーは ODBC *3.x*アプリケーションまたは ODBC でコンパイルされるときに、標準に準拠したアプリケーションを*3.x*ヘッダー ファイルし、リンクODBC を使って*3.x*ライブラリ、ODBC を使用してドライバー、アプリケーションがアクセスおよび*3.x*ドライバー マネージャー。  
  
 標準に準拠したアプリケーションとドライバーは、ODBC_STD コンパイル フラグを使用してコンパイルされます。  
  
 標準に準拠したアプリケーションが、次の動作があります。  
  
-   標準に準拠したアプリケーションから呼び出す場合**SQLAllocEnv** (ために発生する**SQLAllocEnv** 、Open Group と ISO CLI の有効な関数は、)、呼び出しにマップされて**SQLAllocHandleStd**コンパイル時にします。 その結果、実行時に、アプリケーション呼び出し**SQLAllocHandleStd**します。 この呼び出しの処理の中には、ドライバー マネージャーは SQL_ATTR_ODBC_VERSION 環境属性を SQL_OV_ODBC3 に設定します。 呼び出し**SQLAllocHandleStd**への呼び出しに相当**SQLAllocHandle**で、 *HandleType* sql_handle_env としてとへの呼び出しの**SQLSetEnvAttr**を SQL_ATTR_ODBC_VERSION を SQL_OV_ODBC3 に設定します。  
  
-   標準に準拠したアプリケーションから呼び出す場合**SQLBindParam** (ために発生する**SQLBindParam**は、Open Group と ISO CLI の有効な関数です)、ODBC *3.x*ドライバー マネージャーで同等の呼び出しへの呼び出しをマップする**SQLBindParameter**します。 (を参照してください[SQLBindParam のマッピング](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)付録 g:ドライバーに関するガイドラインの下位互換性です。)  
  
-   ISO cli で、ODBC に合わせて*3.x*ヘッダー ファイルへの呼び出しで使用される情報の種類の別名を含む**SQLGetInfo**します。 標準に準拠したアプリケーションは、これらの別名を使用して、ODBC ではなく*3.x*情報の種類。 詳細については、次のトピックを参照してください。[ヘッダー ファイル](../../../odbc/reference/develop-app/header-files.md)します。  
  
-   標準に準拠したアプリケーションで動作するドライバーでサポートするすべての機能がサポートされていることを確認してください。 SQL_SCROLLABLE と設定を SQL_ATTR_CURSOR_SCROLLABLE ステートメント属性を設定 SQL_INSENSITIVE または SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY ステートメント属性は、標準のオプション機能として利用可能な機能ODBC で含まれていない*3.x*コア レベルと可能性がありますでサポートされていないすべての ODBC *3.x*ドライバー。 標準に準拠したアプリケーションは、これらの機能を使用している場合、ドライバーでは動作をサポートしていることを確認する必要があります。
