---
title: データ ソースの仕様のサブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fae642b46b4c652583622ec4832b3217d0b1681c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068563"
---
# <a name="data-source-specification-subkeys"></a>データ ソースの仕様のサブキー
ODBC データ ソースのサブキーに表示されている各データ ソースには、独自のサブキーがあります。 このサブキーは、ODBC データ ソースのサブキーの下の対応する値として同じ名前を持ちます。 このサブキーの下の値は、ドライバ DLL の一覧を表示する必要があり、データ ソースの説明が表示されます。 ドライバーは、翻訳者をサポートする場合、値は既定の変換を既定のトランスレーター DLL、および既定の変換オプションの名前を一覧表示可能性があります。 値はドライバーによってデータ ソースに接続するために必要なその他の情報も一覧表示します。 たとえば、ドライバーでは、サーバー名、データベース名、またはスキーマ名を必要があります。  
  
 値の形式は、次の表に示すようにします。 ドライバーの値のみが必要です。  
  
|名前|データ型|data|  
|----------|---------------|----------|  
|説明|REG_SZ|*description*|  
|Driver|REG_SZ|*ドライバー DLL のパス*|  
|TranslationDLL|REG_SZ|*トランスレーター DLL のパス*|  
|TranslationName|REG_SZ|*translator-name*|  
|TranslationOption|REG_SZ|*translation-option*|  
|*選択、値の名前*|*選択値型*|*opt-value-data*|  
  
 たとえば、SQL Server ドライバー ANSI への変換からの OEM、サーバー名とフラグが必要ですし、これらのサーバーと OEMTOANSI 値を定義します。 インベントリのデータ ソースが Windows® Latin 1 (1250) および多言語 (850) コード ページ間で変換を Microsoft® コード ページ変換プログラムを使用することもあるとします。 インベントリ サブキーの値が次のようにあります。  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
