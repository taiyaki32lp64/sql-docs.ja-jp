---
title: カーソル ライブラリの操作 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad141939a548aa008ef7109d0adaec5b3a8c6c3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001996"
---
# <a name="cursor-library-operations"></a>カーソル ライブラリの操作
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 場合、ODBC を使用するアプリケーション*2.x*ドライバーは、odbc 呼び出しを行う*3.x*カーソル ライブラリでは、アプリケーションが ODBC を使用することがあります*3.x*れていない機能ODBC でサポートされている*2.x*ドライバー。 アプリケーションの作成者は、これらの機能の使い方、ただし、注意でしなければなりません。 ODBC の使用*3.x*カーソル ライブラリは、ODBC には行いません*2.x*に ODBC ドライバー *3.x*ドライバー。
