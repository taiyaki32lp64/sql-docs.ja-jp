---
title: カタログ関数によって返されるデータ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14499071bd180a7ea709fda3eb26aeae46f229c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077022"
---
# <a name="data-returned-by-catalog-functions"></a>カタログ関数によって返されるデータ
各カタログ関数では、データがその結果セットを返します。 この結果セットが他のすべての結果セットと変わりありません。 通常生成されるパラメーター化によって、定義済み**選択**ドライバーでハードコーディングまたはストアド プロシージャは、データ ソース内にあるステートメント。 結果セットからデータを取得する方法については、次を参照してください。[が、結果セットを作成しますか?](../../../odbc/reference/develop-app/was-a-result-set-created.md)します。  
  
 各カタログ関数の結果セットは、その関数の参照エントリの説明です。 一覧の列だけでなく、結果セットは、最後の定義済みの列の後にドライバー固有の列を含めることができます。 これらの列 (存在する場合) は、ドライバーのドキュメントで説明します。  
  
 アプリケーションでは、結果セットの末尾からの相対ドライバー固有の列をバインドする必要があります。 取得 - 最後の列の数としてドライバー固有の列の数を計算する必要があります、 **SQLNumResultCols** - 必要な列の後に発生した列の数を引いた値。 これにより新しい列が結果に追加されたときに、アプリケーションを変更することは、ODBC のバージョンまたはドライバー将来的に設定します。 操作するには、このパターンの結果セットの末尾からの相対列番号が変わらないように、ドライバーは古いドライバー固有の列の前に、ドライバー固有の新しい列を追加する必要があります。  
  
 特殊文字が含まれている場合でも、結果セットで返される識別子に引用符がないです。 たとえば、識別子を引用符文字とします (特定のドライバーとを通じて返されることが**SQLGetInfo**) 二重引用符 (") は、Accounts Payable の表に、Customer Name という名前の列が含まれています。 によって返される行で**SQLColumns**このコラムでは TABLE_NAME 列の値が Accounts Payable 日、いない"Accounts Payable"、および COLUMN_NAME 列の値は、顧客名、「顧客名ではなく」。 Accounts Payable テーブル内の顧客の名前を取得するには、アプリケーションは、これらの名前を引用符は。  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 詳細については、次を参照してください。[引用符で囲まれた識別子](../../../odbc/reference/develop-app/quoted-identifiers.md)します。  
  
 カタログ関数は、ユーザー名とパスワードに基づいて接続が確立し、ユーザーが特権を持ってデータのみが返される SQL に似た承認モデルに基づきます。 このモデルに適合しません、個々 のファイルのパスワード保護は、ドライバーの定義です。  
  
 カタログ関数によって返される結果セットは更新可能なほとんどないと、アプリケーションは、これらの結果セット内のデータを変更することで、データベースの構造を変更するのには期待できません。
