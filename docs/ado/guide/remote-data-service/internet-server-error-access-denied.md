---
title: 'インターネット サーバー エラー: アクセスが拒否されました |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: MightyPen
ms.author: genemi
ms.openlocfilehash: adbfc4e56c49447d88fb354d1e67c2c5e3e30b71
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922621"
---
# <a name="internet-server-error-access-denied"></a>インターネット サーバー エラー: アクセス拒否
このエラーが発生する場合は、通常、Microsoft インターネット インフォメーション サービス (IIS) で、次の状態が返されることを意味します。  
  
 HTTP_STATUS_DENIED 401  
  
 IIS がアクセスしているディレクトリが適切な権限を持っていることを確認します。 RDS は、次の 3 つのパスワード認証モードのいずれかで実行されている IIS Web サーバーと通信できます。Anonymous、Basic、または NT チャレンジ/レスポンス (Windows 2000 で呼び出されたの統合 Windows 認証)。 また、Web サーバーは、Windows NT または Windows 2000 コンピューターである場合、データ ソースのコンピューターへのアクセス許可が必要です。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="see-also"></a>関連項目  
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)




