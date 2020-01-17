---
title: ドライバーのアーキテクチャの概要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 833c953df3502eb7e5d5676da8df057734174619
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071919"
---
# <a name="driver-architecture-overview"></a>ドライバーのアーキテクチャの概要
Microsoft Visual FoxPro ODBC ドライバーは、32 ビット ドライバーを開き、Microsoft Visual FoxPro データベースまたは開く Database Connectivity (ODBC) インターフェイスを使用して FoxPro テーブルをクエリすることができます。 FoxPro を次の種類のアプリケーションを使用してデータにアクセスできます。  
  
-   Microsoft のクエリを使用して、ODBC との通信に、Microsoft Excel や Microsoft Word などの Microsoft Office アプリケーション。  
  
-   Microsoft Visual C または ODBC SDK API を使用して C# で記述されたアプリケーション。  
  
-   Microsoft Visual Basic または Microsoft Visual Basic for Applications で記述されたアプリケーション。  
  
 各ケースでは、情報の要求は、ODBC API を使用します。 ODBC ドライバー マネージャーを開き、FoxPro テーブルおよびデータベースからデータを取得する Visual FoxPro ODBC ドライバーで動作します。  
  
 アーキテクチャは、次の図で表されます。  
  
 ![ODBC ドライバーのアーキテクチャ](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Visual FoxPro 用語集](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [インストールして、Visual FoxPro ODBC ドライバーの構成](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Visual FoxPro ODBC ドライバーの使用](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
