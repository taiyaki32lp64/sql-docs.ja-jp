---
title: 標準的なプログラミング インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a241ea92af6c1273039cc45daab232a1fbe763a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081839"
---
# <a name="standard-programming-interface"></a>標準のプログラミング インターフェイス
プログラミング インターフェイスが標準化のための最も明らかな候補ではおそらくです。 実際には、ODBC の開発中、時に ANSI および ISO 既に提供されている標準 embedded SQL および SQL モジュール。 SQL アクセス グループのデータベース ベンダーの業界コンソーシアム - が; を作成するかどうかを考えていたが、データベースの CLI の標準がなかったODBC の後の部分では、作業の基礎となりました。  
  
 ODBC の要件の 1 つが、1 つのアプリケーション バイナリは、複数の Dbms を使用する必要があります。 このための ODBC が埋め込まれた SQL またはモジュールの言語を使用しないことがあります。 埋め込まれた SQL とモジュールの言語の言語は標準化されていますが、各は DBMS 固有 precompilers に関連付けられます。 したがって、各 DBMS 用のアプリケーションを再コンパイルする必要があり、結果のバイナリが 1 つの DBMS でのみ動作します。 ミニコンピューターとメインフレームの世界で検出された量の少ないアプリケーションの許容されるが、余裕がないパーソナル コンピューターの世界でします。 高ボリューム、市販のソフトウェアの複数のバージョンを顧客に配信するロジスティックな悪夢が最初に、次に、パーソナル コンピューターのアプリケーションは、複数の Dbms を同時にアクセスすることがあります。  
  
 コールレベル インターフェイスを実装して、ライブラリ、または各ローカル コンピューター上に存在するデータベース ドライバーを通じてその一方で、別のドライバーは、各 DBMS 必要があります。 単一のアプリケーションが再コンパイルしないで、さまざまな Dbms のデータにアクセスできるおよびからデータにアクセスできますので、最新のオペレーティング システムでは、実行時に (Microsoft® Windows® オペレーティング システム上のダイナミック リンク ライブラリ) など、このようなライブラリを読み込むことができます、同時には複数をデータベースします。 データベースの新しいドライバーが利用可能になるようユーザーだけインストールできます各自のコンピューターでこれらの変更、再コンパイル、またはデータベース アプリケーションを再リンクする必要はありません。 に、呼び出しレベルのインターフェイスが ODBC の候補がさらに、Windows のプラットフォームを対象の ODBC が開発された、このようなライブラリの広範な使用が既に行われています。
