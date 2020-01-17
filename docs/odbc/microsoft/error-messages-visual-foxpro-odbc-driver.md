---
title: エラー メッセージ (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6072a6e317ab87118376b08790fc0fb49c495e3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952514"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>エラー メッセージ (Visual FoxPro ODBC ドライバー)
エラーが発生する場合、Visual FoxPro ドライバーは、次の情報を返します。  
  
-   ネイティブ エラー番号とエラー メッセージ テキスト  
  
-   SQLSTATE (ODBC エラー コード) とエラー メッセージ テキスト  
  
 呼び出すことによってこのエラーの情報にアクセスする[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)します。  
  
## <a name="native-errors"></a>ネイティブ エラー  
 データ ソースで発生するエラーの場合は、Visual FoxPro ドライバーは、ネイティブ エラー番号とエラー メッセージ テキストを返します。 ネイティブ エラー番号の一覧は、次を参照してください。 [Visual FoxPro ODBC ドライバー ネイティブのエラー メッセージ](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)します。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC エラー コード)  
 検出され、Visual FoxPro ドライバーによって返されるエラーの場合は、ドライバーは、返されたネイティブ エラー番号を適切な SQLSTATE にマップします。 ネイティブ エラー番号にマップする ODBC エラー コードを持たない場合、Visual FoxPro ドライバーは SQLSTATE S1000 を返します (一般的なエラー)。  
  
 対応する Visual FoxPro エラー Visual FoxPro ODBC ドライバーによって生成された、SQLSTATE 値の一覧は、次を参照してください。 [ODBC エラー コード](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)します。  
  
## <a name="syntax"></a>構文  
 エラー メッセージには、次の形式があります。  
  
 **[** *vendor* **][** *ODBC_component* **]** *error_message*  
  
 角かっこ () 内のプレフィックスは、次の表で定義されているように、エラーの原因を確認します。  
  
|データ ソース|Prefix|値|  
|-----------------|------------|-----------|  
|ドライバー マネージャー|[ベンダー]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC ドライバー マネージャー]<br />なし|  
|Visual FoxPro ドライバー|仕入先]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Visual FoxPro の ODBC driver]<br />なし|  
  
 たとえば、Visual FoxPro ODBC ドライバーがファイル employee.dbf を見つけられなかった場合、次のエラー メッセージを返す可能性があります。  
  
 "[*Microsoft*] [*ODBC Visual FoxPro ドライバー*] 'employee.dbf' ファイルが存在しない"
