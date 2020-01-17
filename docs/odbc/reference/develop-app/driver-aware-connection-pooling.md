---
title: ドライバー対応接続プール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dee7ee2b08e4b3b0249ede7f999cfb23d8db944
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047047"
---
# <a name="driver-aware-connection-pooling"></a>ドライバー対応接続プール
ドライバー対応接続プールは、Windows 8 のドライバー マネージャーの新しい機能です。 ドライバー対応接続プールには、接続プールの ODBC ドライバーでの動作をカスタマイズするためにドライバー作成者が使用できます。  
  
> [!NOTE]  
>  ドライバー対応接続プールは、カーソル ライブラリではサポートされていません。 アプリケーションとドライバー対応接続プールが有効にすると、SQLSetConnectAttr を使用してカーソル ライブラリを有効にするとエラー メッセージが表示されます。  
  
 ドライバー対応接続がプールのアドレスは次の問題は、ドライバー マネージャーの接続プールに関連します。  
  
 **プールの断片化**ドライバー マネージャーは、のみ、新しい接続要求の接続文字列と正確に一致の場合、プールからの接続を返しますが。  ドライバー マネージャーの完全一致を要求する理由の 1 つは、ドライバー マネージャーは、すべてのドライバー固有の接続文字列キーワードと値には理解しません。  ただし、ドライバー (正確な時刻の差は、データ ソースによって異なります) の新しい接続を開くために必要な時間未満でデータベースを変更することができますので、いくつか (など、データベースの名前)、接続文字列のキーワード値には、完全に一致する可能性があります不要です。 また、いくつかの接続属性 SQL_ATTR_CURRENT_CATALOG) などの違いがより (SQL_ATTR_LOGIN_TIMEOUT) などの他の属性内の相違点を変更する時間がかかることができます。 ドライバー マネージャーをコストが低い、再利用可能な接続をプールから使用されないようにするも。 多くの新しい接続を作成する場合、ドライバー、アプリケーションのパフォーマンスが低下することができ、データ ソースのスケーラビリティを減らすことができます。 ドライバー対応接続プールをドライバーがより正確に接続要求をプール内の接続を再利用のコストを見積もるためには、プールの断片化を削減できます。  
  
 **アプリケーションの基本設定のならず**一部のデータ ソースは効率的に新しい接続を開きます (いくつかの属性をリセットすると比較して) ため、アプリケーションが若干不一致を再利用しようとしています代わりに新しい接続を開きたい場合があります。プールとリセットのいくつかの値 (ただし低速接続プールの初期化のフレーズの中にはこのことがあります) から接続します。 一部のアプリケーションが、サーバーの負荷を小さく、正しい動作の不一致を修正する大きなコストがある可能性がありますが、接続の数を開きます。 ドライバー対応接続プールなしを指定できません 基本設定のこのような実際には、ドライバー マネージャーがすべてのドライバー固有の接続属性を認識しないため。 ドライバー対応接続プールと、ユーザーの設定に基づいて、プールからの接続を再利用のコストをより正確に見積もることできるように (SQLSetConnectAttr のドライバー固有の属性) を持つユーザーの設定を取得するためのドライバーができます。  
  
 ドライバー対応接続プールの詳細については、次を参照してください。 [ODBC ドライバーで接続プールの認識を開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)します。  
  
## <a name="determining-driver-support"></a>ドライバーのサポートを決定します。  
 ドライバー対応接続プールは、省略可能な機能ドライバーがサポートされていない可能性があります。 ドライバーが、サポートしているかを判断する、SQL_DRIVER_AWARE_POOLING_SUPPORTED を使用して、*情報の種類*の[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)します。  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>ドライバー対応接続プールを有効にする方法  
 アプリケーションは、ドライバーの接続プールの認識を使用して、SQL_CP_DRIVER_AWARE に SQL_ATTR_CONNECTION_POOLING 属性を設定して[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)します。 ドライバー マネージャーの接続プールが使用するドライバー対応接続プールをサポートしていない場合 (SQL_CP_DRIVER_AWARE ではなく SQL_CP_ONE_PER_HENV も指定されている場合と同じ)。 ODBC 2.x と 3.x アプリケーションには、この機能が有効にすることができます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
