---
title: 結果セットのメタデータ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d8da8c15c861fff4767aa598e1b989d8f699c95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020590"
---
# <a name="result-set-metadata"></a>結果セットのメタデータ
*メタデータ*はその他のデータを表すデータです。 たとえば、結果セットのメタデータには、結果セット内の列の数、それらの列、その名前、有効桁数、null 許容属性、およびなどのデータ型など、結果セットがについて説明します。  
  
 相互運用可能なアプリケーションでは、結果セット列のメタデータを常に確認する必要があります。 カタログ関数によって返される、列のメタデータから結果セット内の列のメタデータが異なる場合があります。 たとえば、2 つのテーブルを結合して作成された結果セットで、更新可能な列が含まれているとします。 中に**SQLColumnPrivileges**ユーザーは、列を更新できますを結果セットのメタデータが列の結合の「多」側でない場合がある可能性があります多くのデータ ソースではなく、結合の"一"側の列を更新できます、"。多"側です。 データ型もできないと想定されますは同じであるため、データ ソースは、結果セットを作成するときに、データ型を昇格する可能性があります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [メタデータの使用方法](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol および SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
