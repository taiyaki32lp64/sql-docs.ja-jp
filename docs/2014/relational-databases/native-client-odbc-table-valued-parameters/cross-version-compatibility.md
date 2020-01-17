---
title: 複数バージョンの互換性 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f23b0f43b32d737f03cb7c9b00368558e89e9288
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199995"
---
# <a name="cross-version-compatibility"></a>複数バージョン間の互換性
  バージョン間の競合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のクライアント インスタンスまたはサーバー インスタンスでテーブル値パラメーターを処理する必要がある場合に発生することがあります。  
  
 一般に、テーブル値パラメーターの機能を使用できるのは、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (以降) のサーバーに接続されている [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のクライアント (SQL Server Native Client 10.0 を使用) だけです。 カタログ関数の結果セットの新しい列はのみに接続されているときに表示されます、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (またはそれ以降) サーバー。  
  
 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client でコンパイルされたクライアント アプリケーションで、テーブル値パラメーターが必要なステートメントを実行すると、サーバーではデータ変換エラーからこの状態が検出され、ODBC によって、これが "データ型の属性に関する制限に違反しました" というメッセージの SQLSTATE 07006 として返されます。  
  
 場合、クライアント アプリケーションでコンパイルされた[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 10.0 またはサーバー インスタンスに接続されているときに、テーブル値パラメーターを使用する以降の試行よりも前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client が、これを検出し、SQLBindCol、SQLBindParameter、SQLSetDescFields、および SQLSetDescRec 呼び出しは「データ型の属性違反 (この接続の SQL Server のバージョンではテーブル値パラメーターはサポートされません) の制限」とメッセージの SQLSTATE 07006 で失敗します。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
