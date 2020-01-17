---
title: システム要件、アドレスの予約アプリケーション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2450cc97229a6629d4c2895f3960e3033d129789
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922036"
---
# <a name="system-requirements-for-the-address-book-application"></a>アドレス帳アプリケーションのシステム要件
アドレス帳のサンプル アプリケーションをセットアップするには、次のソフトウェアとデータベースの要件を満たす必要があります。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="software-requirements"></a>ソフトウェア要件  
 この Web アプリケーションを実行するためのサーバー コンピューターのソフトウェア要件は次のとおりです。  
  
-   Microsoft Windows NT® Server 4.0、Service Pack 3 以降または Microsoft Windows® 2000 Server。  
  
-   Microsoft インターネット インフォメーション サービス (IIS) バージョン 3.0 以降、Active Server Pages を使用します。  
  
 この Web アプリケーションを実行するためのクライアント コンピューターのソフトウェア要件は次のとおりです。  
  
-   Microsoft Internet Explorer 4.0 またはそれ以降。  
  
-   Microsoft Windows NT 4.0 のワークステーションまたはサーバー、Windows 2000、または Microsoft Windows 98 です。  
  
## <a name="database-requirements"></a>データベース要件  
 このサンプルを使用するには、が必要です。  
  
-   運用上の Microsoft® SQL Server バージョン 6.5 以降のデータベース サーバーを使用して。  
  
-   データベースを作成し、サンプル データを追加する特権。  
  
-   Enterprise Manager または ISQL ユーティリティ (SQL Server 7.0 で呼び出されたクエリ アナライザー) を使用して設定されたデータを検証します。  
  
 特権がいない場合、データベース管理者は、システムおよびアクセス許可をデータベースまたはデータベースを設定することを設定する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [アドレス帳の SQL スクリプトを実行します。](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [アドレス帳のサンプル アプリケーションの実行](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


