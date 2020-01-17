---
title: ODBC ドライバーのサブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eb54ba7becad42d8d9d2c2870c02db37a3c7d89f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093982"
---
# <a name="odbc-drivers-subkey"></a>ODBC ドライバーのサブキー
ODBC ドライバーのサブキーの下の値には、インストールされているドライバーが一覧表示します。 これらの値の形式は、次の表に示します。  
  
|名前|データ型|data|  
|----------|---------------|----------|  
|*ドライバーの説明*|REG_SZ|**インストールされています。**|  
  
 *ドライバー説明*名は、ドライバーの開発者によって定義されます。 これは通常、ドライバーに関連付けられている DBMS の名前です。  
  
 たとえば、書式設定されたテキスト ファイルと SQL Server のドライバーがインストールされているとします。 ODBC ドライバーのサブキーの下の値は次のようになります。  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
