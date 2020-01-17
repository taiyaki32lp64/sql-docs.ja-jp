---
title: Sql-92 準拠 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5d8ed2818b466d16591be8b70478221d7ac84df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063367"
---
# <a name="sql-92-compliance"></a>SQL-92 準拠
ODBC のデスクトップ データベース ドライバーと、基になる Microsoft Jet エンジンは、sql-92 準拠ではありません。 Sql-92 で定義されている多くの機能をサポートしています。 ドライバーでサポートされている一部の機能は、sql-92 ではサポートされていません。 詳細については、次を参照してください。、 *Microsoft Jet データベース エンジン プログラマー ガイド*します。 次に、2 つの主な違いを示します。  
  
-   デスクトップ データベース ドライバーで使用される SQL より強力な SQL 92 によって指定された式がサポートしています。  
  
-   BETWEEN の述語にさまざまなルールが適用されます。  
  
-   デスクトップ データベース ドライバーと ANSI SQL で使用される SQL には、別のキーワードがサポートしています。  
  
 次の SQL 92 機能は、Microsoft Jet SQL ではサポートされません。  
  
-   GRANT やロックなどのセキュリティ ステートメント。  
  
-   DISTINCT 集計関数の参照。  
  
 次の機能は、sql-92 で指定されていないデスクトップ データベース ドライバーで使用される SQL での機能強化です。  
  
-   TRANSFORM ステートメントは、クロス集計クエリのサポートを提供します。  
  
-   その他の集計関数 (**StDev**と**VarP**)。  
  
> [!NOTE]  
>  デスクトップ データベース ドライバーの標準の ANSI 構文から % (パーセント) と _ (アンダー スコア) のいないサポート * (アスタリスク) としますか? (疑問符) に設定します。
