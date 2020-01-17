---
title: 検索ステートメントの構築 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8f24fe59da1377ea42900a8f1f0b89eb97125f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019167"
---
# <a name="constructing-searched-statements"></a>検索ステートメントの構築
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 位置付けされた更新および削除ステートメントをサポートするために、カーソルライブラリは位置付けされたステートメントから検索された  **UPDATE** または **DELETE** ステートメントを作成します。 データ・ブロック内で **SQLGetData** への呼び出しをサポートするために、カーソル・ライブラリーは検索された **SELECT** ステートメントを構成して、現在のデータ行を含む結果セットを作成します。 これらの各ステートメントで、**WHERE** 句 は、**SQLColAttribute** 内のSQL_DESC_SEARCHABLEフィールドIDにSQL_PRED_SEARCHABLEまたはSQL_PRED_BASICを戻す各バインド列について、キャッシュに格納されている値を列挙します。  
  
> [!CAUTION]  
>  現在の行を識別するためにカーソル ライブラリによって構築された **WHERE** 句は、任意の行の識別、異なる行の識別、または複数の行の識別に失敗する可能性があります。  
  
 位置指定の update または delete ステートメントを 1 つ以上の行に影響する場合、カーソル ライブラリをカーソルが配置されている、SQL_SUCCESS_WITH_INFO と SQLSTATE 01001 (カーソル操作の競合) を返しますの行のみの行の状態配列を更新します。 ステートメントで行が識別されない場合、カーソル ライブラリは行の状態配列を更新できませんし、SQL_SUCCESS_WITH_INFO と SQLSTATE 01001 (カーソル操作の競合) を返します。 アプリケーションが呼び出すことができます**SQLRowCount**更新または削除された行の数を決定します。  
  
 **SQLGetData** の呼び出しにカーソルを配置するために使用する **SELECT** が複数の行を識別する場合、**SQLGetData** は正しいデータを返すことが保証されていません。 すべての行を特定できない場合は、**SQLGetData** は sql_no_data を返します。  
  
 アプリケーションが次のガイドラインに準拠している場合、カーソル ライブラリによって構築された**WHERE** 句は、データソースに重複する行が含まれている場合など、不可能な場合を除いて、現在の行を一意に識別します。  
  
-   **行を一意に識別する列をバインドします。** バインドされた列が行を一意に識別しない場合、カーソルライブラリによって構築された**WHERE** 句は複数の行を識別することがあります。 位置付けされた UPDATE および DELETE ステートメントでは、そのような句によって複数の行が更新または削除される可能性があります。 **SQLGetData** の呼び出しでは、そのような句が誤った行のデータを返すことがあります。 すべての列を一意のキーにバインドすると、各行が一意に識別されます。 一意のキーですべての列をバインドには、各行は一意に識別されていることが保証されます。  
  
-   **切り捨てが発生しないように、十分な大きさのデータ バッファーを割り当てます。** カーソル ライブラリのキャッシュは、**SQLBindCol** で結果セットにバインドされた行セットバッファ内の値のコピーです。 これらのバッファーに配置されているときにデータが切り捨てられる場合、キャッシュにも切り捨てられます。 切り捨てられた値から構築された**WHERE** 句 はデータ ソースの基になる行を正しく認識しない可能性があります。  
  
-   **バイナリーCデータには、null 以外の長さのバッファーを指定します。** **SQLBindCol** の *StrLen_or_IndPtr* 引数が null 以外の場合にのみ、カーソル ライブラリはキャッシュに長さバッファーを割り当てます。 *TargetType* 引数がSQL_C_BINARY の場合、カーソルライブラリは、データから **WHERE** 句を構築するためにバイナリデータの長さを必要とします。 SQL_C_BINARY 列用の長さバッファーがなく、アプリケーションが **SQLGetData** を呼び出すか、位置指定 UPDATE または DELETE ステートメントを実行しようとすると、カーソル ライブラリはSQL_ERROR と SQLSTATE SL014 を返します（位置指定要求が出され、すべての列数のフィールドがバッファーに格納されません）。  
  
-   **Null 許容の列に null 以外の長さのバッファーを指定します。** **SQLBindCol** の *StrLen_or_IndPtr* 引数が null 以外の場合にのみ、カーソル ライブラリはキャッシュに長さバッファーを割り当てます。 SQL_NULL_DATA は長さバッファーに保管されているため、カーソル ライブラリは、バッファーが指定されている長さのないの任意の列が null 非許容であると仮定します。 Null 許容列長の列が指定されていない場合、カーソル ライブラリはその列のデータ値を使用する **WHERE** 句を構成します。 この句は、行を正しく識別しません。
