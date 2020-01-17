---
title: 仕様のサブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec94f3e02b720617e8f7369b12a916c2bbbe7b16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093804"
---
# <a name="translator-specification-subkeys"></a>ドライバーの仕様のサブキー
ODBC トランスレーターのサブキーで表示されている各翻訳には、独自のサブキーがあります。 このサブキーは、ODBC トランスレーターのサブキーの下の対応する値として同じ名前を持ちます。 このサブキーの下の値は、翻訳者とトランスレーター セットアップ Dll と使用率カウントの完全なパスを一覧表示します。 値の形式は、次の表に示すようにします。  
  
|名前|データ型|data|  
|----------|---------------|----------|  
|[変換者]|REG_SZ|*トランスレーター DLL のパス*|  
|セットアップ|REG_SZ|*セットアップ DLL へのパス*|  
|UsageCount|REG_DWORD|*count*|  
  
 使用状況カウントの詳細については、次を参照してください。[使用状況のカウント](../../../odbc/reference/install/usage-counting.md)このセクションで前述しました。  
  
 アプリケーションでは、使用率カウントは設定しないでください。 ODBC では、この数を維持します。  
  
 たとえば、Microsoft のコード ページの翻訳者が翻訳 Mscpxl32.dll、トランスレーター セットアップの機能が同じの DLL に含まれるという名前の DLL と 3 回、変換プログラムがインストールされているとします。 Microsoft コード ページのトランスレーターのサブキーの下の値が次のようにあります。  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
