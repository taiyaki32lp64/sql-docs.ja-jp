---
title: SQLFetch (カーソル ライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2cb829f065421a13d3c7df06c670808bc3d9d77c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064431"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLFetch**カーソル ライブラリ内の関数。 に関する一般的な情報**SQLFetch**を参照してください[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)します。  
  
 カーソル ライブラリを使用すると、呼び出し**SQLFetch**いずれかへの呼び出しを混在させることはできません**SQLFetchScroll**または**SQLExtendedFetch**します。  
  
 場合**SQLFetch**呼びますドライバーへの呼び出しを渡す際に、カーソル ライブラリで SQL_ATTR_ROW_ARRAY_SIZE を 1 より大きい値に設定を使用します。 ドライバーが、ODBC 2 の場合は。*x*ドライバー、行セットのサイズは無視されますとへの呼び出し**SQLFetch**は 1 行のデータを返します。  
  
 場合は、カーソル ライブラリは、ODBC 2 で使用されます。*x*ドライバー、オフセット (SQL_ATTR_ROW_BIND_OFFSET_PTR ステートメント属性で定義) されたバインドがない場合に使用**SQLFetch**が呼び出されます。  
  
 アプリケーションが呼び出すことはできません、カーソル ライブラリが読み込まれるときに**SQLFetch**ブックマーク列をフェッチします。 カーソル ライブラリへの呼び出しに渡します**SQLFetch**を介して、ドライバーが、関数にブックマークを有効にして、ブックマーク列をバインドする呼び出しを受け取り、カーソル ライブラリ。
