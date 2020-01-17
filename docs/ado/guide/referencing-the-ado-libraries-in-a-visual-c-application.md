---
title: Visual C アプリケーションで ADO ライブラリを参照する |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 62fb1b89299af1f466e446c8adba422a841f0196
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923024"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Visual C++ アプリケーションで ADO ライブラリを参照する
Visual C アプリケーションでの ADO の最新バージョンを使用するには、次を使用して`#import`ディレクティブ。  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 ADO MD または ADOX を使用することをインポートする必要があります*msadomd.dll*または*msadox.dll*、上記の構文を使用しています。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ADO の以前のバージョンを使用する置換*msado15.dll*上で次のタイプ ライブラリのいずれか。  
  
-   *msado27.tlb*、ADO 2.7 タイプ ライブラリ  
  
-   *msado26.tlb*、ADO 2.6 のタイプ ライブラリ  
  
-   *msado25.tlb*、ADO 2.5 のタイプ ライブラリ  
  
-   *msado21.tlb*、ADO 2.1 のタイプ ライブラリ  
  
-   *msado20.tlb*、ADO 2.0 のタイプ ライブラリ
