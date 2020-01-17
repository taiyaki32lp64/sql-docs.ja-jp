---
title: 相対と絶対のスクロール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e2034a3922dcd3db77113e08a6c48fe7ac39457f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138057"
---
# <a name="relative-and-absolute-scrolling"></a>相対と絶対のスクロール
スクロール オプションのほとんど**SQLFetchScroll**絶対位置または現在位置を基準にカーソルを配置します。 **SQLFetchScroll** 、次のフェッチをサポートしています前に、最初と最後の行セットとしても相対パスとしてをフェッチしています (行セットをフェッチ*n*現在の行セットの先頭からの行) と絶対フェッチ (フェッチ、行セットの開始。行の*n*)。 場合*n*は行が結果セットの最後から数えられます絶対フェッチで負の値。 そのため、行-1 の絶対フェッチは、結果セットの最後の行で始まる行セットをフェッチすることです。  
  
 動的カーソルに挿入および動的カーソルの速度が低下する可能性が、結果セットの先頭から読み取り以外の特定の数の行を取得する簡単な方法はありませんので、結果セットから削除された行を検出します。 さらに、絶対フェッチは動的カーソルで非常に便利な行番号を変更する行の挿入や削除されたため、そのため、連続して同数の行をフェッチするいますと別の行が生成することができます。  
  
 使用するアプリケーション**SQLFetchScroll**ブロックに対してのみ、レポートなどのカーソル機能は、一度に 1 つを結果セットを通過する可能性がありますオプションのみを使用して、次の行セットをフェッチします。 スクリーン ベースのアプリケーションでは、その一方で、活用することのすべての機能**SQLFetchScroll**します。 スクロール バーの操作への呼び出しを直接変換できる場合は、アプリケーションでは、行セットのサイズを画面に表示される行の数に設定し、結果セットに、画面バッファーをバインドする、 **SQLFetchScroll**します。  
  
|スクロール バーの操作|SQLFetchScroll のスクロール操作|  
|--------------------------|-------------------------------------|  
|1 画面分上へ移動 (PageUp)|SQL_FETCH_PRIOR|  
|1 画面分下へ移動 (PageDown)|SQL_FETCH_NEXT|  
|1 行上へ移動|指定した SQL_FETCH_RELATIVE *FetchOffset*を-1 に等しくないです。|  
|1 行下へ移動|指定した SQL_FETCH_RELATIVE *FetchOffset*を 1 に等しい|  
|上部にあるスクロール ボックス|SQL_FETCH_FIRST|  
|下部のスクロール ボックス|SQL_FETCH_LAST|  
|スクロール ボックスを任意の位置に移動|SQL_FETCH_ABSOLUTE|  
  
 このようなアプリケーションも、現在の行番号と行の数が必要ですが、スクロール操作の後のスクロール ボックスを配置する必要があります。 現在の行番号のアプリケーションかを監視できる、現在の行番号または呼び出し**SQLGetStmtAttr** SQL_ATTR_ROW_NUMBER 属性を取得します。  
  
 結果のサイズであると、カーソル内の行の数を設定、診断のヘッダーの SQL_DIAG_CURSOR_ROW_COUNT フィールドとして使用できます。 このフィールドの値が後でのみ定義されている**SQLExecute**、 **SQLExecDirect**、または**SQLMoreResult**が呼び出されました。 この数には、カウントの概数またはドライバーの機能によって、正確な数のいずれかを指定できます。 ドライバーのサポートを呼び出すことによって決まりますできます**SQLGetInfo**カーソルの属性情報の種類とカーソルの種類に SQL_CA2_CRC_APPROXIMATE または SQL_CA2_CRC_EXACT ビットを返すかどうかを確認します。  
  
 動的カーソルの正確な行数がサポートされていることはありません。 他の種類のカーソルでは、ドライバーは、真数または概数値の行の数が両方をサポートできます。 おおよそも正確なドライバーがサポートしている場合は、行を特定のカーソルの種類のカウント、SQL_DIAG_CURSOR_ROW_COUNT フィールドが、これまでにフェッチされる行の数が含まれています。 どのようなドライバーをサポートするのに関係なく**SQLFetchScroll**で、*操作*SQL_FETCH_LAST が原因で SQL_DIAG_CURSOR_ROW_COUNT フィールドに正確な行の数を格納します。
