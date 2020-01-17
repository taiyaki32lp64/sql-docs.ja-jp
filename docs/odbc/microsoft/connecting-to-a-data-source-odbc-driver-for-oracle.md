---
title: データ ソース (ODBC Driver for Oracle) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0e9e62c8e03166ec2f76b1c6bcb5000a062bac3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082037"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>データ ソース (ODBC Driver for Oracle) への接続
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 ODBC アプリケーションでは、さまざまな方法で接続情報を渡すことができます。 など、アプリケーションでは、ドライバーの接続情報のユーザーを常に確認する場合があります。 または、アプリケーションがデータ ソース接続を指定する接続文字列を期待します。 データ ソースに接続する方法は、ODBC アプリケーションで使用される接続方法によって異なります。  
  
 データ ソースに接続する 1 つの一般的な方法では、データ ソース ダイアログ ボックスを使用します。 ODBC アプリケーションは、ダイアログ ボックスを使用するセットアップは場合、そのダイアログ ボックスが表示され、適切なデータ ソースの接続情報をユーザーに求めます。  
  
 使用してデータ ソースに接続することも、[接続文字列](../../odbc/microsoft/connection-string-format-and-attributes.md)します。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>ダイアログ ボックスを使用してデータ ソースに接続するには  
  
1.  データ ソース ダイアログ ボックスが表示されたらは、Oracle データ ソースを選択し、ok をクリックします。 接続 ダイアログ ボックスが表示されます。  
  
2.  [接続] ダイアログ ボックスの適切な情報を入力し、[ok] をクリックします。  
  
 接続情報の確認は、アプリケーションは、ODBC Driver for Oracle を使用してデータ ソースに含まれる情報にアクセスすることができます。
