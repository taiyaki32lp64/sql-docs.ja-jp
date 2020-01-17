---
title: Read Repeatable 分離レベルを使用したデッドロック |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8e4e59606f3b68fbd9ce272db8ea8a50ab53e88
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922714"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>Read Repeatable 分離レベルでのデッドロック
カスタム ビジネス オブジェクトでは、repeatable read 分離レベルを使用して、SQL Server にアクセスして、クエリを送信し、同じトランザクションで更新する 2 つのクライアントで同時にビジネス オブジェクトを呼び出す、デッドロックは可能性があります。 デッドロックを解除する際にタイムアウトするプロセスのいずれかを許可するリモート データ サービスは設計されていますが、そのクライアントの更新プログラムが失敗します。  
  
 使用して、[カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)**コマンド タイムアウト**タイムアウトの長さを変更する動的プロパティ。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="see-also"></a>関連項目  
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)



