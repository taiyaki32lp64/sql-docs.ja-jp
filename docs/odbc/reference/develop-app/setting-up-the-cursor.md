---
title: カーソルの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c47e534f069f810948189f2668d4ecdfbfa4ad79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107543"
---
# <a name="setting-up-the-cursor"></a>カーソルの設定
設定の結果を作成するステートメントを実行する前に、アプリケーションは、カーソルの種類を指定できます。 これは、SQL_ATTR_CURSOR_TYPE ステートメント属性を持つ。 アプリケーションが、型が明示的に指定しない場合は、順方向専用カーソルが使用されます。 混合カーソルを取得するには、アプリケーションは、キーセット ドリブン カーソルを指定しますが、結果セットのサイズより小さいキーセットのサイズを宣言します。  
  
 キーセット ドリブン、混合カーソルの場合、アプリケーションは、キーセットのサイズにも指定できます。 これは、SQL_ATTR_KEYSET_SIZE ステートメント属性を持つ。 キーセットのサイズが 0 で、既定値に設定されている場合は、キーセットのサイズは、結果セットのサイズに設定され、キーセット ドリブン カーソルが使用されます。 カーソルが開かれた後、キーセットのサイズを変更できます。  
  
 アプリケーションでは、行セットのサイズを設定できますまた詳細については、次を参照してください。[ブロック カーソルを使用して](../../../odbc/reference/develop-app/using-block-cursors.md)、このセクションでは以前のバージョン。
