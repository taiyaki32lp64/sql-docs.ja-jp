---
title: ドライバーに直接接続する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44b9de304069849e965fc335e130ae57d9ec8bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083162"
---
# <a name="connecting-directly-to-drivers"></a>ドライバーに直接接続する
説明したとおり[データ ソースまたはドライバーを選択する](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)、このセクションで前述した一部のアプリケーションは、データ ソースをまったく使用しません。 代わりに、ドライバーに直接接続します。 **SQLDriverConnect**アプリケーションがデータ ソースを指定せずに、ドライバーに直接接続する方法を提供します。 概念的には、一時的なデータ ソースは、実行時に作成されます。  
  
 ドライバーに直接接続する場合、アプリケーションを指定します、**ドライバー**の代わりに、接続文字列キーワードで、 **DSN**キーワード。 値、**ドライバー**キーワードは、ドライバーの説明、によって返される**SQLDrivers**します。 たとえば、ドライバーは Paradox ドライバーの説明があるため、データ ファイルを含むディレクトリの名前が必要です。 このドライバーに接続するには、アプリケーションは次の接続文字列のいずれかで使用可能性があります。  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 最初の文字列で、ドライバーはその他の情報を必要はありません。 2 番目の文字列で、ドライバーは、データ ファイルを含むディレクトリの名前を要求する必要があります。
