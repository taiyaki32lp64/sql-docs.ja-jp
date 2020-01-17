---
title: ODBC 接続プール オプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43d4fe1ab363326269daf40375e126b930d2548b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901641"
---
# <a name="setting-odbc-connection-pooling-options"></a>ODBC 接続プール オプションの設定
接続プールを使用するアプリケーションを使用するたびに再確立する必要がない接続プールから接続を使用します。 使用することができます、**接続プール**のタブ、 **ODBC データ ソース アドミニストレーター**  ダイアログ ボックスを有効にし、パフォーマンスの監視を無効にします。 接続タイムアウト期間を設定するドライバー名をダブルクリックします。  
  
 ドライバー レベルでは、接続プールは CPTimeout レジストリの値で有効にします。 接続プールがサポートするドライバーだけを有効にするシステム管理者は、有効にするこのドライバーごとのオプションを選択できます。 これは、ドライバーのセットアップ プログラムの中に CPTimeout の既定値の設定によって実現されます。 接続タイムアウト期間を設定するドライバー名をダブルクリックします。  
  
 接続プールの詳細については、次を参照してください。 [ODBC 接続プーリング](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)します。  
  
## <a name="performance-monitoring"></a>パフォーマンス監視  
 さまざまな統計情報を記録することによって接続のパフォーマンスを追跡するパフォーマンスを監視します。 これらの統計情報は、次の項目を含める開発者によってカスタマイズできます。  
  
|カウンター|定義|  
|-------------|----------------|  
|1 秒あたりの ODBC ハード接続カウンター|サーバーに行われた 1 秒あたりの実際の接続の数。 初めて環境内の実行、負荷の高いこのカウンターは移動非常に簡単にします。 、数秒後に 0 にそれが削除されます。 これは、接続プールが動作しているときに通常の状況です。 サーバーへの接続が確立されるが使用され再利用するため、プール内に配置します。|  
|ODBC ハード カウンター 1 秒あたりの切断します。|ハードの数 1 秒間のサーバーに発行を切断します。 これらは、サーバーには、接続のプールでリリースされる実際の接続です。 この値は 0 に高くなります、システム上のすべてのクライアントを停止すると、接続がタイムアウトに開始します。|  
|1 秒あたりの ODBC 接続の論理的なカウンター|秒で、その他語をからの接続プールあたりのプールでなければ接続の数が、ユーザーに渡されます。 このカウンターは、プールが動作しているかどうかを示します。 サーバーで、負荷に応じて 1 秒あたり 40 ~ 60 の論理的な接続を表示することも珍しくはされません。|  
|1 秒あたりの ODBC ソフト切断カウンター|アプリケーションによって発行された 1 秒あたりの数を切断します。 アプリケーションのリリースまたは切断、プールに戻り、接続が配置されます。|  
|ODBC の現在アクティブな接続のカウンター|現在使用されている、プール内の接続の数。|  
|ODBC 現在無料接続カウンター|現在、プールで使用可能な無料の接続数。 これらは、使用可能なライブ接続です。|  
|現在アクティブなプールします。|現在アクティブなプールの数。 このカウンターは、接続プール内の接続を管理するドライバーに対して、Windows 8 で追加されました。 詳細については、次を参照してください。[ドライバー対応接続プール](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)します。|  
|作成されたプール|アクティブで、アクティブ、削除されたプールを含むプールの数。 このカウンターは、接続プール内の接続を管理するドライバーに対して、Windows 8 で追加されました。 詳細については、次を参照してください。[ドライバー対応接続プール](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)します。|  
  
 独自の監視パラメーターを指定する必要があります。 パフォーマンスを監視するためのサンプルは、このバージョンの ODBC に組み込まれています。
