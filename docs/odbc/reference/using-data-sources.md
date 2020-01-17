---
title: データ ソースの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52015cb202f46c50c16dcab408bed7761f0925db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951801"
---
# <a name="using-data-sources"></a>データ ソースの使用
通常、データ ソースが、エンドユーザーによって作成、またはプログラムでの技術者と呼ばれる、 *ODBC アドミニストレーター*します。 Odbc データ ソース アドミニストレーターでは、ドライバーを使用するユーザーを要求、そのドライバーを呼び出します。 ドライバーでは、データ ソースに接続するために必要な情報を要求するダイアログ ボックスが表示されます。 ユーザー情報を入力すると、ドライバーは、システムでそれを格納します。  
  
 後で、アプリケーションでは、ドライバー マネージャーを呼び出すし、コンピューターのデータ ソースの名前またはファイル データ ソースを含むファイルのパスを渡します。 マシンのデータ ソース名が渡された場合、ドライバー マネージャーは、データ ソースで使用するドライバーを検索するシステムを検索します。 ドライバーを読み込み、データ ソース名を渡します。 ドライバーでは、データ ソース名を使用して、データ ソースに接続するために必要な情報を見つけます。 最後に、通常のユーザー ID とパスワード、通常、保存されていないユーザーに確認、データ ソースに接続します。  
  
 ファイルのデータ ソースを渡されるときに、ドライバー マネージャーはファイルを開き、指定されたドライバーを読み込みます。 場合は、ファイルには、接続文字列も含まれています、ドライバーにこれを渡します。 接続文字列に情報を使用して、ドライバーは、データ ソースに接続します。 接続文字列が渡されなかった場合、ドライバーは一般にユーザーに必要な情報を求めます。
