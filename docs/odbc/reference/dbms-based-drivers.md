---
title: DBMS ベースのドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcd2221d9a0bb9cba42745901e5f00a6f8c8415e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111249"
---
# <a name="dbms-based-drivers"></a>DBMS ベースのドライバー
DBMS ベースのドライバーはドライバーを使用するためのスタンドアロン データベース エンジンを提供する、Oracle または SQL Server などのデータ ソースで使用されます。 これらのドライバー、スタンドアロンのエンジンです。 物理データにアクセスします。これは、SQL ステートメントを送信し、エンジンから結果を取得します。  
  
 DBMS ベースのドライバーは、既存のデータベース エンジンを使用して、ため、通常は簡単にファイル ベースのドライバーよりも記述されます。 DBMS ベースのドライバーは、ネイティブの API 呼び出しに ODBC 呼び出しを変換することによって簡単に実装、低速のドライバーでこの結果します。 DBMS ベースのドライバーを実装する優れた方法では、ネイティブ API の動作は、通常は基になるデータ ストリーム プロトコルを使用します。 たとえば、SQL Server ドライバーは、Db-library (SQL Server のネイティブ API) ではなく TDS (データは、SQL Server のプロトコルをストリーミング) を使用してください。 この規則の例外は、ODBC がネイティブの API である場合です。 たとえば、Watcom SQL は、スタンドアロン アプリケーションと同じコンピューター上に存在し、ドライバーとして直接読み込まれるエンジンです。  
  
 DBMS ベースのドライバーは、データ ソースをサーバーとして機能する、クライアント/サーバー構成でクライアントとして機能します。 ほとんどの場合、クライアント (ドライバー) とサーバー (データ ソース) 上に存在さまざまなコンピューターは、マルチタスクのオペレーティング システムを実行している同じコンピューター上の両方でしたが。 3 番目の方法としては、*ゲートウェイ、* ドライバーとデータ ソースの間にします。 ゲートウェイは、別のように 1 つの DBMS を原因となるソフトウェアです。 たとえば、SQL Server を使用するアプリケーション データにアクセスできます DB2 マイクロ Decisionware DB2 ゲートウェイ; 経由この製品により、DB2 から SQL Server のようになります。  
  
 次の図は、DBMS に基づいたドライバーの 3 つの異なる構成を示します。 最初の構成で、ドライバーとデータ ソースが同じコンピューターに存在します。 次に、ドライバーとデータ ソースは、異なるコンピューターに存在します。 第 3 回目、ドライバーとデータ ソースが異なるコンピューター上に存在し、ゲートウェイがまだ別のコンピューター上にあるそれらの間に配置します。  
  
 ![DBMS の 3 つの構成&#45;ベースのドライバー](../../odbc/reference/media/pr07.gif "pr07")
