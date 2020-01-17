---
title: トレース DLL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6fe910c93beac676e5fb0f663b740c03a826c326
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985224"
---
# <a name="trace-dll"></a>トレース DLL
トレースを実行する DLL では、ODBC コア コンポーネントの 1 つです。 以前、DLL、Windows SDK の ODBC コンポーネントでサンプル DLL として現在提供されているしがトレースには、Microsoft Data Access Components (MDAC) SDK が含まれています。 したがって、レジストリ エントリ、インターフェイス、およびトレース DLL 用のサンプル コードは、使用します。 この DLL は、DLL を ODBC ユーザーまたはサード パーティ ベンダーによって生成されたトレースで置き換えられます。 カスタム トレース DLL には、元のサンプル トレース DLL とは異なる名前を指定する必要があります。 トレース Dll はシステム ディレクトリにインストールする必要があります。 または読み込みが失敗します。 接続文字列は渡されませんトレース DLL をドライバー マネージャーによって。  
  
 トレース DLL は、入力引数、出力引数、引数の遅延、リターン コード、および SQLSTATEs をトレースします。 ドライバー マネージャーが 2 つの点でトレース DLL を呼び出すトレースが有効にすると: (引数の検証) の前に関数の開始時に 1 回、もう一度だけ、関数が戻る前にします。  
  
 アプリケーションは、関数を呼び出すときに、ドライバー マネージャーは、ドライバーで、関数の呼び出しまたは呼び出し自体を処理する前に DLL のトレースでトレース関数を呼び出します。 各 ODBC 関数が、対応するトレース関数 (付いて*トレース*) は、名前を除く、ODBC 関数と同じです。 トレース関数が呼び出されると、トレース DLL は、入力引数をキャプチャし、リターン コードを返します。 ドライバー マネージャーは、引数を検証する前に、トレース DLL を呼び出すと、無効な関数呼び出しのトレースため、ため、状態遷移のエラーと無効な引数がログに記録されます。  
  
 トレース DLL でトレース関数を呼び出した後は、ドライバー マネージャーは、ドライバーの ODBC 関数を呼び出します。 呼び出して**TraceReturn**トレース DLL にします。 この関数は 2 つの引数を受け取ります。 トレース関数の場合、トレース DLL によって返される値と、ODBC 関数のドライバー マネージャーに、ドライバーによって返されるリターン コード (または、関数を処理した場合、ドライバー マネージャーによって自体が返される値)。 関数では、トレース機能は、返される値を使用して、キャプチャされた入力引数の値を操作します。 ODBC 関数のログ ファイルに返されるコードを書き込みます (または有効になっている場合、動的に表示されます)。 出力引数へのポインターを逆参照し、出力引数値は、ログに記録します。
