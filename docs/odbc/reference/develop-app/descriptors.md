---
title: 記述子 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2138a5f8417fc9156c916719e96d707b9a29de9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040011"
---
# <a name="descriptors"></a>記述子
記述子ハンドルは、列または動的パラメーターのいずれかに関する情報を保持するデータ構造を表します。  
  
 暗黙的に列とパラメーターのデータを操作する ODBC 関数を設定および記述子フィールドを取得します。 たとえば、 **SQLBindCol**と呼びます列のデータをバインドするバインディングを完全に記述する記述子フィールドを設定します。 ときに**SQLColAttribute**と呼ばれる列のデータを記述する記述子フィールドに格納されたデータを返します。  
  
 ODBC 関数を呼び出すアプリケーションでは、記述子で考慮する必要があります。 アプリケーションが記述子への直接アクセスを取得するデータベースの操作は不要です。 ただし、一部のアプリケーションは、多くの操作を合理化記述子に直接アクセスできます。 記述子へのアクセスは、列のデータは、呼び出すよりも効率的に再バインドする方法を提供します。 たとえば、直接**SQLBindCol**もう一度です。  
  
> [!NOTE]  
>  記述子の物理的に表したものが定義されていません。 アプリケーションは、記述子ハンドルを使用して ODBC 関数を呼び出すことによってそのフィールドを操作することによってのみ、記述子への直接アクセスを利用できます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [記述子の種類](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [記述子フィールド](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [記述子の割り当てと解放](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [記述子フィールドの取得と設定](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
