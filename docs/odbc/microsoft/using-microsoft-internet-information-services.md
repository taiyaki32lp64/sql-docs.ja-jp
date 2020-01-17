---
title: Microsoft インターネット インフォメーション サービスを使用して |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e531149af21facd80e9e6ddab19a76c3bdc0fa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088141"
---
# <a name="using-microsoft-internet-information-services"></a>Microsoft インターネット インフォメーション サービスの使用
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 ある場合 (特に ORA 12641 エラーが発生する) 場合は、IIS スクリプト内からの接続に問題は、Sqlnet.ora ファイルに次の行を追加します。  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 匿名認証を使用して接続するために、これがセキュリティで保護されたネットワーク サービスを無効になります。
