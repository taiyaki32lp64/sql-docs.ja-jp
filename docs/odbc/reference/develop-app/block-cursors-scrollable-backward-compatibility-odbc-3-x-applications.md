---
title: ブロックと ODBC のカーソルのスクロール可能な互換性 3.x |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d12906f8dec0bfb12fc861c067e6e615e758a3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134987"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>ODBC 3.x アプリケーション用のブロック カーソル、スクロール可能なカーソル、および下位互換性
両方が存在する**SQLFetchScroll**と**SQLExtendedFetch** odbc の間で、アプリケーション プログラミング インターフェイス (API)、一連の関数である最初の平文の分割は、アプリケーションの呼び出し、およびサービス プロバイダー インターフェイス (SPI) 関数のセットである、ドライバーが実装されます。 この分割は ODBC の要件のバランスを取るために必要な*3.x*、使用する**SQLFetchScroll**に、標準の連携して、ODBC との互換性、 *2.x*、使用します。**SQLExtendedFetch**します。  
  
 ODBC *3.x*は API のセットにアプリケーション呼び出しの機能が含まれています**SQLFetchScroll**および関連するステートメント属性。 ODBC *3.x* 、SPI は、セットである関数のドライバーを実装して、含まれています**SQLFetchScroll**、 **SQLExtendedFetch**、および関連するステートメント属性。 ODBC は、この分割、API と SPI を正式には適用されません、ため、ODBC のことが*3.x*を呼び出すアプリケーション**SQLExtendedFetch**および関連するステートメント属性。 ただし、ODBC の理由はありません*3.x*これを行うアプリケーション。 Api および Spi の詳細についてはの概要を参照してください。 [ODBC アーキテクチャ](../../../odbc/reference/odbc-architecture.md)します。  
  
 方法については、ODBC *3.x*ドライバー マネージャーは odbc 呼び出しをマッピング*2.x*および ODBC *3.x*ドライバー、およびどのような関数とステートメント属性 ODBC *3.x*ドライバーがブロックとスクロール可能なカーソルを実装する必要がありますを参照してください[、ドライバーが何](../../../odbc/reference/appendixes/what-the-driver-does.md)で付録 g:旧バージョンとの互換性のためのガイドラインをドライバーです。  
  
 次の表に、どのような機能とステートメント属性 ODBC *3.x*ブロックとカーソルのスクロール可能なアプリケーションを使用する必要があります。 ODBC の間での変更も一覧表示されます*2.x*および ODBC *3.x*この領域でその ODBC *3.x* ODBC と互換性がある注意すべきアプリケーション*2.x。* ドライバー。  
  
|関数または<br /><br /> ステートメント属性|コメント|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|使用したブックマークを指す**SQLFetchScroll**します。<br /><br /> ときに、ODBC でのアプリケーション設定この*2.x*ドライバー、固定長のブックマークをポイントする必要があります。|  
|SQL_ATTR_ROW_STATUS_PTR|埋められた行の状態配列を指す**SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations**、および**SQLSetPos**します。<br /><br /> アプリケーションの ODBC でこれが設定されている場合*2.x*ドライバーと呼び出し**SQLBulkOperation**で、*操作*の呼び出しの前に SQL_ADD **SQLFetchScroll**、 **SQLFetch**、または**SQLExtendedFetch**、SQLSTATE HY011 (属性はここで設定することはできません) が返されます。<br /><br /> アプリケーションを呼び出すと**SQLFetch** odbc *2.x*ドライバー、 **SQLFetch**にマップされて**SQLExtendedFetch**のでこの配列内の値。|  
|SQL_ATTR_ROWS_FETCHED_PTR|バッファーを指す**SQLFetch**と**SQLFetchScroll**フェッチされた行の数を返します。<br /><br /> アプリケーションを呼び出すと**SQLFetch** odbc *2.x*ドライバー、 **SQLFetch**にマップされて**SQLExtendedFetch**ので、このバッファー内の値。|  
|SQL_ATTR_ROW_ARRAY_SIZE|行セットのサイズを設定します。<br /><br /> アプリケーションを呼び出す場合**SQLBulkOperations**で、*操作*odbc SQL_ADD の*2.x*呼び出し、SQL_ATTR_ROW_ARRAY_ いないドライバー、SQL_ROWSET_SIZE が使用されますサイズの呼び出しにマップされて**SQLSetPos**で、*操作*、SQL_ADD SQL_ROWSET_SIZE を使用するのです。<br /><br /> 呼び出す**SQLSetPos**で、*操作*SQL_ADD のまたは**SQLExtendedFetch** odbc *2.x*ドライバーは SQL_ROWSET_SIZE を使用します。<br /><br /> 呼び出す**SQLFetch**または**SQLFetchScroll** odbc *2.x*ドライバーは、SQL_ATTR_ROW_ARRAY_SIZE を使用します。|  
|**SQLBulkOperations**|挿入とブックマークの操作を実行します。 ときに**SQLBulkOperations**で、*操作*SQL_ADD の ODBC で呼び出される*2.x*ドライバーにマップされます**SQLSetPos** で*操作*SQL_ADD の。 次に、実装の詳細を示します。<br /><br /> -ODBC の使用時に*2.x*ドライバー、アプリケーションに関連付けられている、暗黙的に割り当てられた ARD のみを使用する必要があります、 *StatementHandle*; ため、行を追加するため別 ARD を割り当てることができません、明示的な記述子の操作は、ODBC でサポートされていない*2.x*ドライバー。 アプリケーションを使用する必要があります**SQLBindCol**されません、ARD にバインドする**SQLSetDescField**または**SQLSetDescRec**します。<br />-ODBC の呼び出し時に*3.x*ドライバー、アプリケーションが呼び出すことができます**SQLBulkOperations**で、*操作*の呼び出しの前に SQL_ADD **SQLFetch**または**SQLFetchScroll**します。 ODBC の呼び出し時に*2.x*ドライバー、アプリケーションが呼び出す必要があります**SQLFetchScroll**呼び出す前に**SQLBulkOperations**操作の SQL_ADD とします。|  
|**SQLFetch**|次の行セットを返します。 次に、実装の詳細を示します。<br /><br /> のアプリケーションを呼び出すと**SQLFetch** odbc *2.x*にマップされたドライバー、 **SQLExtendedFetch**します。<br />のアプリケーションを呼び出すと**SQLFetch** odbc *3.x* SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性で指定された行の番号を返すドライバー。|  
|**SQLFetchScroll**|指定した行セットを返します。 次に、実装の詳細を示します。<br /><br /> のアプリケーションを呼び出すと**SQLFetchScroll** odbc *2.x*ドライバー、SQLSTATE 01S01 を返します (行内のエラー) の 1 行に適用される各エラーの前にします。 だけであるためこれは、ODBC *3.x*ドライバー マネージャーをマップする**SQLExtendedFetch**と**SQLExtendedFetch**この SQLSTATE を返します。 アプリケーションを呼び出すと**SQLFetchScroll** odbc *3.x*ドライバー、決して返します SQLSTATE 01S01 (行内のエラー)。<br />のアプリケーションを呼び出すと**SQLFetchScroll** odbc *2.x*ドライバー *FetchOrientation* SQL_FETCH_BOOKMARK に設定、 *FetchOffset*引数を 0 に設定する必要があります。 SQLSTATE HYC00 オフセットに基づくブックマークをフェッチしていますが、ODBC で試行された場合は、(省略可能な機能が実装されていません) が返されます。 *2.x*ドライバー。|  
  
> [!NOTE]  
>  ODBC *3.x*アプリケーションは使用しないでください**SQLExtendedFetch**または SQL_ROWSET_SIZE ステートメントの属性。 代わりに、使用する必要があります**SQLFetchScroll**と SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性。 ODBC *3.x*アプリケーションは使用しないでください**SQLSetPos**で、*操作*SQL_ADD の使用する必要がありますが、 **SQLBulkOperations** で*操作*SQL_ADD の。
