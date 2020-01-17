---
title: SQLSTATE (ODBC エラー コード) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 253841e26ab7ecbeafb2cfeeed8c090c91650d14
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62805866"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC エラー コード)
  SQLSTATE は、警告やエラーの原因についての詳細情報を提供します。 データで発生するエラーのソースが検出され、によって返される[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、返されたネイティブ エラー番号を適切な SQLSTATE にマップします。 ネイティブ エラー番号をマップできる ODBC エラー コードを持たない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは SQLSTATE 42000 (「構文エラーまたはアクセス違反です」) を返します。 ドライバーで検出されたエラーのため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが適切な SQLSTATE を生成します。  
  
 状態エラー コードの詳細については、次のトピックを参照してください。  
  
-   [付録 A: ODBC エラー コード](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE マッピング](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>参照  
 [エラーとメッセージの処理](handling-errors-and-messages.md)  
  
  
