---
title: ドライバーのアーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd9bbb74d77a0b56b6b1f1aa5d8f1a6b5e97f5aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915470"
---
# <a name="driver-architecture"></a>ドライバーのアーキテクチャ
ドライバーのアーキテクチャは、どのソフトウェア プロセス SQL ステートメントによって、2 つのカテゴリに分類されます。  
  
-   **ファイル ベースのドライバー**ドライバーは、物理的なデータを直接アクセスします。 この場合、ドライバーは、ドライバーとデータ ソースの両方としては機能します。つまり、ODBC 呼び出しと SQL ステートメントを処理します。 たとえば、dBASE ドライバーは、dBASE がスタンドアロン データベース エンジン、ドライバーを使用できますを提供しないために、ファイル ベースのドライバーです。 ファイル ベースのドライバーの開発者が独自のデータベース エンジンを記述する必要がありますに注意してください。 重要です。  
  
-   **DBMS ベースのドライバー**ドライバーを別のデータベース エンジンを介して物理データにアクセスします。 ここでドライバーが ODBC 呼び出しのみを処理します。SQL ステートメントに渡すには、データベース エンジンを処理します。 たとえば、Oracle ドライバーは、Oracle のドライバーを使用してスタンドアロンのデータベース エンジンのため、DBMS に基づいたドライバーです。 データベース エンジンが存在する場所は重要ではありません。 ドライバーと同じコンピューターまたはネットワーク上の別のコンピューターに常駐できます。ゲートウェイを経由でもアクセス可能性があります。  
  
 一般に、ドライバーの作成者だけに興味深いは、ドライバーのアーキテクチャつまり、ドライバーのアーキテクチャ一般に違いはありませんアプリケーション。 ただし、アーキテクチャは、アプリケーションは DBMS 固有の SQL を使用できるかどうかにできます。 たとえば、Microsoft Access では、スタンドアロン データベース エンジンを提供します。 Microsoft Access ドライバーでは、DBMS ベース - - このエンジンを介してデータにアクセスする場合、アプリケーションは Microsoft Access、SQL ステートメントを処理エンジンに渡すことができます。  
  
 ただし、ドライバーでは、ファイルベースでは、Microsoft® Access .mdb ファイルを直接にアクセスする独自のエンジンが含まれている場合、Microsoft Access 固有の SQL ステートメントをエンジンに渡すしようとするとは構文エラーが発生する可能性があります。 理由は、独自のエンジンが ODBC SQL のみを実装する可能性が高いことです。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ファイル ベースのドライバー](../../odbc/reference/file-based-drivers.md)  
  
-   [DBMS ベースのドライバー](../../odbc/reference/dbms-based-drivers.md)  
  
-   [ネットワークの例](../../odbc/reference/network-example.md)  
  
-   [その他のドライバーのアーキテクチャ](../../odbc/reference/other-driver-architectures.md)
