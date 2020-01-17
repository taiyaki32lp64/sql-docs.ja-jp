---
title: ODBC Core サブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c9380083eb5a0ad796f436af271564676b757d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094009"
---
# <a name="odbc-core-subkey"></a>ODBC Core サブキー
ODBC Core サブキーの値では、コア コンポーネント (ドライバー マネージャー、カーソル ライブラリ、インストーラー DLL、およびなど) の使用率カウントを示します。 この値の形式は、次の表に示します。  
  
|名前|データ型|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*count*|  
  
 たとえば、ODBC コア コンポーネントは、次の 3 つの異なるアプリケーションと 2 つの異なるドライバーのセットアップ プログラムによってインストールされているとします。 ODBC Core サブキーの値は次のようになります。  
  
```  
UsageCount : REG_DWORD : 0x5  
```
