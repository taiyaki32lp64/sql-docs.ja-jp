---
title: 標準モードとコンテキスト接続に関する制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
ms.openlocfilehash: d8cbdd195f698090602b98cdb6e5bab0a86556ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216409"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>コンテキスト接続と通常の接続 - 制限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックで説明して実行するコードに関する制限事項、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]コンテキストと通常の接続を処理します。  
  
## <a name="restrictions-on-context-connections"></a>コンテキスト接続に関する制限事項  
 アプリケーションを開発するときは、コンテキスト接続に適用される次の制限事項を考慮してください。  
  
-   特定の接続に対して特定の時点に開くことができるコンテキスト接続は 1 つだけです。 複数のステートメントをそれぞれ独立した接続で同時に実行する場合、その中の 1 つの接続しか独自のコンテキスト接続を取得できません。 この制限事項は、異なる接続からの同時実行要求には影響しません。つまり、特定の接続の特定の要求にしか影響しません。  
  
-   コンテキスト接続では、MARS (複数のアクティブな結果セット) がサポートされません。  
  
-   **SqlBulkCopy**クラスは、コンテキスト接続では動作しません。  
  
-   コンテキスト接続では、更新バッチ処理がサポートされません。  
  
-   **SqlNotificationRequest**コンテキスト接続に対して実行するコマンドでは使用できません。  
  
-   コンテキスト接続に対して実行しているコマンドはキャンセルできません。 **SqlCommand.Cancel**メソッドは、要求をサイレント モードでは無視されます。  
  
-   "context connection=true" を使用する場合は、他の接続文字列キーワードを使用できません。  
  
-   **SqlConnection.DataSource**プロパティの接続文字列の場合は null を返します、 **SqlConnection**は"コンテキスト接続 = true"のインスタンスの名前ではなく[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。  
  
-   設定、 **SqlCommand.CommandTimeout**プロパティには効果がないコンテキスト接続に対してコマンドを実行します。  
  
## <a name="restrictions-on-regular-connections"></a>通常の接続に関する制限事項  
 アプリケーションを開発するときは、通常の接続に適用される次の制限事項を考慮してください。  
  
-   内部サーバーに対する非同期コマンドの実行はサポートされません。 含む"async = true"のコマンドを実行して、接続文字列で、コマンドの結果で**System.NotSupportedException**がスローされます。 このメッセージが表示されます。"内部で実行される非同期処理はサポートされていません、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]プロセスです"。  
  
-   **SqlDependency**オブジェクトはサポートされていません。  
  
## <a name="see-also"></a>関連項目  
 [コンテキスト接続](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
