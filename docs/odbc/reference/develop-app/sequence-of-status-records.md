---
title: 状態レコードのシーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 67eac22a630305f32f141ea18861e5638445f19b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094347"
---
# <a name="sequence-of-status-records"></a>状態レコードのシーケンス
2 つ以上の状態レコードが返された場合、ドライバー マネージャーとドライバーのランク付け、次の規則に従ってします。 最高のランクを持つレコードは、最初のレコードです。 (ドライバー マネージャー、ドライバー、ゲートウェイ、およびなど) のレコードのソースとは見なされませんときにレコードを順位付けします。  
  
-   **エラー**最高ランクであるエラーを記述した状態レコード。 エラーのレコード間では、トランザクションの失敗または可能なトランザクションの失敗を示すレコードは、他のすべてのレコードを outrank します。 2 つまたは複数のレコードには、同じエラー条件について説明します、SQLSTATEs、開いているグループ CLI 仕様 (HZ で使用するクラス 03) で定義は ODBC 定義およびドライバー定義 SQLSTATEs を outrank します。  
  
-   **データ値の No の実装で定義された**No Data 値 (クラス 02) のドライバーの定義を記述する状態レコードがある 2 番目の最高ランク。  
  
-   **警告**警告 (クラス 01) を示す状態レコード最低ランクであります。 2 つまたは複数のレコードについて警告 SQLSTATEs 開いてグループ CLI 仕様によって定義されている、同じ警告の状態を説明する場合は、ODBC またはドライバー定義 SQLSTATEs を outrank します。  
  
 最高のランクを持つ 2 つ以上のレコードがある場合は、どのレコードが最初のレコードは未定義です。 その他のすべてのレコードの順序は定義されません。 具体的には、エラーの前に警告が表示されるため、関数に関係なく SQL_SUCCESS 以外の値が返されるときに、アプリケーションは状態レコードをすべて確認する必要があります。
