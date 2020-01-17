---
title: ODBC カーソル ライブラリ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a896a5bb41c5530c65573fa22c418199a043f8fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114067"
---
# <a name="the-odbc-cursor-library"></a>ODBC カーソル ライブラリ
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 ブロックとスクロール可能なカーソルは、多くのアプリケーションに非常に便利な追加機能です。 ただし、必ずしもすべてのドライバーは、ブロックとスクロール可能なカーソルをサポートします。 同じ位置指定更新の場合は true、および delete ステートメントと**SQLSetPos**、データの更新についてはします。 そのため、以前に、Microsoft Data Access Components (MDAC)、SDK に含まれる、Windows SDK の ODBC コンポーネントには、カーソル ライブラリが含まれています。 ブロック、静的カーソル、位置指定の update および delete ステートメントの場合、カーソル ライブラリを実装して**SQLSetPos**開いているグループの標準的な CLI への準拠レベルを満たす任意のドライバー用です。 カーソル ライブラリは、ODBC アプリケーションと共に再配布できる可能性があります。詳細については、SDK のライセンス契約を参照してください。  
  
 カーソル ライブラリを使用するには、アプリケーションは、データ ソースに接続する前に SQL_ATTR_ODBC_CURSORS 接続属性を設定します。 カーソル ライブラリの詳細については、次を参照してください[付録 f:。ODBC カーソル ライブラリ](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)します。
