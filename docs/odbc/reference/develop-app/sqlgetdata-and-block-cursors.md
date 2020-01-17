---
title: SQLGetData およびブロック カーソル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4841d8d923ff73d187569df3d7f9e29daf0f4e48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107397"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData およびブロック カーソル
**SQLGetData**は 1 つの行の 1 つの列を操作し、複数の行からデータを格納する配列をフェッチできません。 これは、プライマリの使用のため**SQLGetData**パートでは、長い形式のデータをフェッチするには、一度に 1 つ以上の行に対して行うほとんどまたはまったくない理由があるとします。  
  
 使用する**SQLGetData**アプリケーションの最初の呼び出しをブロック カーソル、 **SQLSetPos**に単一の行にカーソルを移動します。 呼び出して**SQLGetData**内の該当する行の列にします。 ただし、この動作は省略可能です。 ドライバーの使用をサポートしているかどうか**SQLGetData**アプリケーションを呼び出すと、ブロック カーソルと**SQLGetInfo** SQL_GETDATA_EXTENSIONS オプションを使用します。
