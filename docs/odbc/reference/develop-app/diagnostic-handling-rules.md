---
title: 診断処理規則 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 269e021d3fd4610c2fccda46bcd8ca160982543c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039919"
---
# <a name="diagnostic-handling-rules"></a>診断の処理規則
次の規則は、診断の処理で**SQLGetDiagRec**と**SQLGetDiagField**します。  
  
 すべての ODBC コンポーネント。  
  
-   必要がありますいないを交換して、変更、またはエラーまたは警告のもう 1 つの ODBC コンポーネントから受信したマスク。  
  
-   別の ODBC コンポーネントから、診断メッセージを受け取ったとき、追加の状態レコードを追加する可能性があります。 追加したレコードは、実際の情報値を元のメッセージに追加する必要があります。  
  
 ODBC のコンポーネントは、データ ソースを直接インターフェイスします。  
  
-   仕入先、識別子、そのコンポーネントの識別子、および診断メッセージをデータ ソースから受信するデータ ソースの識別子を付ける必要があります。  
  
-   データ ソースのネイティブ エラー コードを保持する必要があります。  
  
-   データ ソースの診断メッセージを保持する必要があります。  
  
 ODBC コンポーネントのエラーまたは警告に関係なく、データ ソースを生成します。  
  
-   エラーまたは警告の適切な SQLSTATE を指定する必要があります。  
  
-   診断メッセージのテキストを生成する必要があります。  
  
-   その仕入先識別子と、診断メッセージにそのコンポーネントの識別子を付ける必要があります。  
  
-   いずれかが使用可能で意味のある場合は、ネイティブ エラー コードを返す必要があります。  
  
 ODBC コンポーネントのドライバー マネージャーと連携します。  
  
-   出力引数を初期化する必要があります**SQLGetDiagRec**と**SQLGetDiagField**します。  
  
-   書式設定し、の出力引数としての診断情報を返す必要があります**SQLGetDiagRec**と**SQLGetDiagField**その関数が呼び出された場合。  
  
 1 つ ODBC ドライバー マネージャー以外のコンポーネント。  
  
-   ネイティブ エラーに基づいて SQLSTATE を設定する必要があります。 ファイル ベースのドライバーとゲートウェイを使用しない DBMS ベースのドライバーは、ドライバーは SQLSTATE を設定する必要があります。 ゲートウェイを使用して、DBMS ベースのドライバー、ドライバーまたは ODBC をサポートするゲートウェイのいずれかが、SQLSTATE を設定できます。
