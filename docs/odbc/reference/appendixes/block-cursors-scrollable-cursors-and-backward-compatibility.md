---
title: ブロック カーソル、スクロール可能なカーソル、および旧バージョンとの互換性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 433647481b2b73c22e00657c430d98177d3d4524
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125224"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>ブロック カーソル、スクロール可能なカーソル、および下位互換性
両方が存在する**SQLFetchScroll**と**SQLExtendedFetch** odbc の間で、アプリケーション プログラミング インターフェイス (API)、一連の関数である最初の平文の分割は、アプリケーションの呼び出し、およびサービス プロバイダー インターフェイス (SPI) 関数のセットである、ドライバーが実装されます。 この分割が必要なように ODBC *3.x*、使用する**SQLFetchScroll**、標準 bealigned も ODBC と互換性があると*2.x*を使用して**SQLExtendedFetch**します。  
  
 ODBC *3.x*は API のセットにアプリケーション呼び出しの機能が含まれています**SQLFetchScroll**および関連するステートメント属性。 ODBC *3.x* 、SPI は、セットである関数のドライバーを実装して、含まれています**SQLFetchScroll**、 **SQLExtendedFetch**、および関連するステートメント属性。 ODBC は、この分割、API と SPI を正式には適用されません、ため、ODBC のことが*3.x*を呼び出すアプリケーション**SQLExtendedFetch**および関連するステートメント属性。 ただし、ODBC の理由はありません*3.x*これを行うアプリケーション。 Api および Spi の詳細についてはの概要を参照してください。 [ODBC アーキテクチャ](../../../odbc/reference/odbc-architecture.md)します。  
  
 関数とステートメントの詳細については、ODBC を属性の*3.x*アプリケーションがブロックとスクロール可能なカーソルを使用する必要がありますを参照してください[ブロック カーソル、スクロール可能なカーソル、および ODBC 用の旧バージョンとの互換性 3.xアプリケーション](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ドライバー マネージャーの機能](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [ドライバーの機能](../../../odbc/reference/appendixes/what-the-driver-does.md)
