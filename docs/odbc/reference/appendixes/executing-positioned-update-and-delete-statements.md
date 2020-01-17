---
title: 位置指定更新と Delete ステートメントの実行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c69f784c2ce7c29cb49c81bf23f34a9cad12089
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913627"
---
# <a name="executing-positioned-update-and-delete-statements"></a>位置指定更新と Delete ステートメントの実行
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 アプリケーションでデータのブロックをフェッチした後、 **SQLFetchScroll**、更新またはブロック内のデータを削除します。 位置指定更新または削除、アプリケーションを実行します。  
  
1.  呼び出し**SQLSetPos**に更新または削除する行にカーソルを移動します。  
  
2.  位置指定の update または delete ステートメントで次の構文を構築します。  
  
     **UPDATE** *table-name*  
  
     **設定** *列識別子* **=** {*式*&#124; です。**NULL**}  
  
     [ **、** *列識別子* **=** {*式*&#124; です。**NULL**}]  
  
     **WHERE CURRENT OF** *カーソル名*  
  
     **DELETE FROM** *テーブル名* **WHERE CURRENT OF** *カーソル名*  
  
     作成する最も簡単な方法、**設定**位置指定の update ステートメントの句は、各列に対してパラメーター マーカーを使用して更新し、使用する**SQLBindParameter**これらの行セットのバッファーをバインドする、更新する行。 この場合、パラメーターの C データ型では、行セットのバッファーの C データ型と同じになります。  
  
3.  位置指定の update ステートメントが実行される場合は、現在の行の行セットのバッファーを更新します。 位置指定の update ステートメントを正常に実行した後は、カーソル ライブラリは、現在の行の各列からそのキャッシュに、値をコピーします。  
  
    > [!CAUTION]  
    >  アプリケーションによって、位置指定の update ステートメントを実行する前に、の行セットのバッファーが正しく更新されない場合、キャッシュ内のデータはできません正しいステートメントを実行した後。  
  
4.  位置指定の update または delete ステートメントがカーソルに関連付けられているステートメントよりも別のステートメントを使用して実行します。  
  
    > [!CAUTION]  
    >  **場所**任意の行を識別する、別の行を特定または複数の行を識別する、現在の行を識別するために、カーソル ライブラリによって構築された句が失敗することができます。 詳細については、次を参照してください。[検索ステートメントの構築](../../../odbc/reference/appendixes/constructing-searched-statements.md)します。  
  
 配置されているすべての更新と delete ステートメントがカーソル名が必要です。 カーソル名を指定するには、アプリケーションが呼び出す**SQLSetCursorName**カーソルが開かれる前にします。 ドライバーによって生成されるカーソル名を使用するアプリケーションを呼び出す**SQLGetCursorName**カーソルが開かれています。  
  
 ライブラリが位置指定更新を実行するカーソルより後または delete ステートメント、状態配列、バッファーの行セット、およびカーソル ライブラリによって保持されるキャッシュは、次の表に示す値を含めることができます。  
  
|ステートメントの使用|行の状態配列内の値します。|内の値<br /><br /> バッファーの行セット|内の値<br /><br /> キャッシュ バッファー|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|位置指定更新を行う|SQL_ROW_UPDATED|新しい値 [1]|新しい値 [1]|  
|位置指定削除|SQL_ROW_DELETED になります|古い値|古い値|  
  
 [1] で、アプリケーションは、位置指定の update ステートメントを実行する前に、行セットのバッファー内の値を更新する必要があります。位置指定の update ステートメントを実行した後は、カーソル ライブラリは、行セットのバッファー内のキャッシュに値をコピーします。
