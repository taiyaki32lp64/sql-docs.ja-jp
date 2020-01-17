---
title: 付録 G :旧バージョンとの互換性のためのドライバーのガイドライン |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a07e936617100c56f8fa873df1b490e1d61e3f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909955"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>付録 G :ドライバーの下位互換性のガイドライン
この付録の内容は、ODBC 3 取り組んでドライバー作成者の情報を提供します。*x* ODBC 2 をサポートするために必要なドライバー *。x*アプリケーション。 旧バージョンと互換性の詳細については、次を参照してください。[旧バージョンとの互換性と標準準拠](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ブロック カーソル、スクロール可能なカーソル、および ODBC 3.x ドライバーとの下位互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)-新しい機能は、ODBC 3 内に存在する機能 *。x* ODBC 2 ではなく *。x*します。 ODBC 3。*x*ドライバー通常必要はありませんので、新機能との下位互換性について心配する ODBC 2 *。x*アプリケーションに使用しないでください。 唯一の例外に関連する機能を**SQLFetch**、 **SQLFetchScroll**、 **SQLSetPos**、および**SQLExtendedFetch**; 詳細についてはについては、この付録の「を参照してください。  
  
-   [非推奨の関数のマップ](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)-重複する機能が ODBC 3 で異なる方法で実装されている機能 *。x*および ODBC 2 *。x*します。 ODBC 3。*x*ドライバーをドライバー マネージャーは、ODBC 2 を常にマップされるため、重複する機能との下位互換性について心配する必要はありません *。x* ODBC 3 に機能します *。x* 、ODBC 3 を呼び出すときに機能します *。x*ドライバー。 したがって、ODBC 3。*x*ドライバーが ODBC 3 のみが表示されます *。x*機能します。 詳細については、これらのマッピング後の「を参照してください。  
  
-   [動作変更および ODBC 3.x ドライバー](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md)の動作の変更が ODBC 3 に異なる方法で処理する機能 *。x*および ODBC 2 *。x*します。 ODBC 3。*x*ドライバーの動作の変更について心配し、応答 SQL_ATTR_ODBC_VERSION 環境属性をアプリケーションで設定する必要があります。
