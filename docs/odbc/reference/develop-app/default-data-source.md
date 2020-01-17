---
title: 既定のデータ ソース |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fb016ac7597617b119834e20ffd9e12bd648dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076847"
---
# <a name="default-data-source"></a>既定のデータ ソース
ドライバーは、特定のケースで、アプリケーションで明示的に指定されない 1 つで、既定のデータ ソースと呼ばれる、データ ソースを選択できます。  
  
-   呼び出しで**SQLConnect**場所、 *ServerName*引数が長さ 0 の文字列、null ポインター、または既定値。  
  
-   呼び出しで**SQLDriverConnect**場所*InConnectionString*いずれかを指定します**DSN**= 既定またはを指定します、 **DSN**キーワード、システム情報に含まれていないデータ ソース。  
  
 ドライバーで定義された既定のデータ ソースを指定する方法。 これは管理操作を伴う可能性があり、ユーザーによって異なります。
