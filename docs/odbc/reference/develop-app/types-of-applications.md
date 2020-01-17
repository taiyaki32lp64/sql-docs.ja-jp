---
title: アプリケーションの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70263b98f6b0e933f8b14fbfa74428c77317f462
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087805"
---
# <a name="types-of-applications"></a>アプリケーションの種類
ODBC アプリケーションは、次のように分類できます。  
  
-   **純粋な ODBC 2。**  
     **_x_アプリケーション**32 ビット アプリケーションです。  
  
    -   ODBC 2 だけを呼び出します。*x*関数 (ODBC 1.0 関数を含む**SQLSetParam**)。 ODBC 1 が含まれます。*x* 32 ビットへ移植されたアプリケーション。  
  
    -   ODBC 2 を想定しています。*x*の動作が変更されている機能の動作。 (を参照してください[動作が変更される](../../../odbc/reference/develop-app/behavioral-changes.md)詳細についてはします)。  
  
    -   再コンパイルされていない ODBC 3.5 ヘッダー。  
  
-   **純粋な ODBC 2。**  
     **_x_アプリケーションの再コンパイル**純粋な ODBC 2 *。x* ODBC 3.5 ヘッダー ファイルを使用して再コンパイルされているアプリケーション 0x0250 = ODBCVER を設定します。  
  
-   **純粋な ODBC 2。**  
     **_x_ Unicode アプリケーション**純粋な ODBC 2 *。x* Unicode 準拠し、SQL_WCHAR データ型を使用するアプリケーションを再コンパイルします。  
  
-   **純粋なグループと ISO**-**ODBC に準拠したアプリケーション**32 ビット アプリケーションです。  
  
    -   グループを開くまたは ISO CLI 標準で定義された関数を呼び出します。 (これらの関数は、非推奨の 3.0 関数を含めることができます)  
  
    -   Unicode データ型を使用しません。  
  
    -   動作が変更されている機能の動作を ODBC 3.0 が必要です。  
  
-   **純粋な ODBC 3.0 アプリケーション**32 ビット アプリケーションです。  
  
    -   3\.0 のヘッダーと共にコンパイルされます。  
  
    -   場合によっては非推奨のものも含めて、すべての ODBC 3.0 関数を呼び出します。  
  
    -   動作が変更されている機能の動作を ODBC 3.0 が必要です。  
  
-   **純粋な ODBC 3.5 アプリケーション**32 または 64 ビット アプリケーションです。  
  
    -   Unicode データ型を使用することがあります。  
  
    -   場合によっては非推奨のものも含めて、すべての ODBC 3.5 関数を呼び出します。  
  
    -   動作が変更されている機能の動作を ODBC 3.5 が必要です。  
  
-   **ODBC 3.8 (またはそれ以降) アプリケーションを純粋な**32 ビットまたは 64 ビット アプリケーションです。  
  
    -   Unicode データ型を使用することがあります。  
  
    -   場合によっては非推奨のものも含めて、すべての ODBC 3.8 関数を呼び出します。  
  
    -   動作が変更されている機能の ODBC 3.8 の動作を期待しています。  
  
-   **アプリケーションの置き換え**32 または 64 ビット アプリケーションです。  
  
    -   重複している機能の新しい動作を実装します。  
  
    -   条件付きコード内でのみ新しいバージョンの ODBC での新しい機能を使用します。  
  
    -   動作の変更を処理する条件付きのコードが限られているまたは以前のバージョンの ODBC アプリケーションに登録されています。
