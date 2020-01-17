---
title: SQLBindParameter (カーソル ライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7943987d52554e0f5cd7723e8c9ae8a0e3afddd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093035"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLBindParameter**カーソル ライブラリ内の関数。 に関する一般的な情報**SQLBindParameter**を参照してください[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)します。  
  
 アプリケーションが呼び出すことができます**SQLBindParameter** C データ型、列のサイズ、およびバインドされた列の 10 進数字の同じ残っている限り、パラメーターを再バインドします。  
  
 カーソル ライブラリでは、バインドのオフセットを使用する SQL_ATTR_ROW_BIND_OFFSET_PTR ステートメント属性の設定をサポートします。 (**SQLBindParameter**呼び出しが発生するこの再バインドする必要はありません)。  
  
 カーソル ライブラリでは、実行時データ パラメーターのバインドをサポートします。
