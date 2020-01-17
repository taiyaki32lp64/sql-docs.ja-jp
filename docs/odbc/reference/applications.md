---
title: アプリケーション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f15b5e8eb6eb7c63ab771030f0c31e8c9ff92724
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135683"
---
# <a name="applications"></a>[アプリケーション]
*アプリケーション*はデータにアクセスする、ODBC API を呼び出すプログラムです。 さまざまな種類のアプリケーションのほとんどが、このガイドで説明する例として使用されている 3 つのカテゴリに分類されます。  
  
-   **汎用アプリケーション**シュリンク ラップされたアプリケーションまたは市販のアプリケーションとして指すこれらもします。 汎用アプリケーションは、さまざまなさまざまな Dbms を使用する設計されています。 例には、スプレッドシートまたは ODBC を使用して、詳細な分析データをインポートする統計情報のパッケージと ODBC を使用してデータベースからメーリング リストを取得するワード プロセッサが含まれます。  
  
     汎用アプリケーションの重要なサブカテゴリは、PowerBuilder、Microsoft® Visual Basic® などのアプリケーションの開発環境です。 これらの環境で構築されたアプリケーションは、おそらく 1 つの DBMS でのみ動作が環境自体は、複数の Dbms を使用する必要があります。  
  
     どのような汎用のすべてのアプリケーションが共通は、Dbms の間で高度に同時には比較的一般的な方法で ODBC を使用して必要なです。 相互運用性に関する詳細については、次を参照してください。[レベルの相互運用を選択する](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)します。  
  
-   **垂直アプリケーション**垂直方向のアプリケーションが注文エントリや、製造データの追跡などのタスクの 1 つの型を実行し、アプリケーションの開発者が制御するデータベース スキーマを使用します。 特定の顧客のアプリケーションは、1 つの DBMS では動作します。 たとえば、小規模なビジネス可能性がありますでアプリケーションを使用 dBase 中、大企業で Oracle を使用することが。  
  
     アプリケーションでは、アプリケーションは、1 つの DBMS に関連付けられていない方法で ODBC が使用されますが、同様の機能を提供する Dbms の数に制限を関連付けることがあります。 したがって、アプリケーション開発者は、DBMS から独立してアプリケーションを販売できます。 垂直方向のアプリケーションは、これらは開発されていますが、顧客が DBMS を選択した後に noninteroperable コードを含むように変更が場合があるときに相互運用可能です。  
  
-   **カスタム アプリケーション**会社の 1 つに、特定のタスクを実行するカスタム アプリケーションを使用します。 たとえば、大企業でのアプリケーションは、(それぞれでさまざまな DBMS は) いくつかの部門から販売データを収集し、1 つのレポートを作成します。 ODBC は、共通のインターフェイスでありから複数のインターフェイスを学習するプログラマを保存するために使用されます。 このようなアプリケーションでは、相互運用可能なは一般に、特定の Dbms とドライバーに書き込まれます。  
  
 タスクの数は、ODBC の使用方法に関係なく、すべてのアプリケーションに共通です。 ODBC アプリケーションのフローをほとんど定義これらをまとめると、します。 タスクは次のとおりです。  
  
-   データ ソースを選択し、接続します。  
  
-   SQL ステートメントの実行を送信しています。  
  
-   (ある場合) は、結果を取得しています。  
  
-   エラーを処理します。  
  
-   コミットまたは SQL ステートメントの外側のトランザクションをロールバックします。  
  
-   データ ソースから切断しています。  
  
 SQL を使用した、ほとんどのデータにアクセスする作業が行われるために、アプリケーションが ODBC を使用する主な作業は、SQL ステートメントを送信し、これらのステートメントによって生成された結果 (指定されている場合) を取得します。 アプリケーションが ODBC を使用するその他のタスクにはの特定しドライバーの機能を調整して、データベース カタログを参照が含まれます。
