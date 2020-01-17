---
title: DCOM 上で実行するように DLL の有効化 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ea7ea83219780602f8d8d68e5c807178e775bc2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922702"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>DCOM 上で実行するための DLL の有効化
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 次の手順では、DCOM とコンポーネント サービスを介して Microsoft インターネット インフォメーション サービス (HTTP) の両方を使用するビジネス オブジェクト .dll を有効にする方法を説明します。  
  
1.  コンポーネント サービス MMC スナップインで新しい空のパッケージを作成します。  
  
     コンポーネント サービス MMC スナップインで使用するパッケージを作成し、このパッケージに DLL を追加します。 これにより、.dll ファイルは、DCOM を使用してアクセスできますが、IIS でのアクセシビリティを削除します。 (.Dll、用にレジストリでチェックする場合、 **Inproc**キーが空になった; の値を追加します、このトピックの後半で説明した、アクティベーション属性を設定、 **Inproc**キー)。  
  
2.  パッケージにビジネス オブジェクトをインストールします。  
  
     \- または -  
  
     インポート、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)パッケージへのオブジェクト。  
  
3.  パッケージのアクティブ化の属性を設定**作成者のプロセスで**(ライブラリ アプリケーション)。  
  
     .Dll を同じコンピューターで DCOM と IIS を介してアクセスできるようにするには、コンポーネント サービス MMC スナップインでコンポーネントのアクティブ化の属性を設定する必要があります。 属性を設定した後**作成者のプロセスで**、表示になります、 **Inproc**コンポーネント サービスへのポインターが .dll をサロゲート サーバーのレジストリ キーが追加されました。  
  
 コンポーネント サービス (または Microsoft トランザクション サービス、Windows NT を使用している場合) の詳細については、次の手順を実行する、Microsoft Transaction Server Web サイトにアクセスする方法。


