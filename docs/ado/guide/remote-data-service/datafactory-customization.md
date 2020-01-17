---
title: DataFactory のカスタマイズ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bdc406778bea0d6355e747998d2517b841fc17b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922776"
---
# <a name="datafactory-customization"></a>DataFactory のカスタマイズ
リモート データ サービス (RDS) は、3 階層のクライアント/サーバー システムでデータ アクセスを簡単に実行する方法を提供します。 クライアントのデータ コントロールは、リモート データ ソース、または接続文字列にクエリを実行する接続とコマンドの文字列パラメーターを指定し、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトの更新プログラムを実行するパラメーター。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 パラメーターは、リモート データ ソースに対するデータ アクセス操作を実行するサーバーのプログラムに渡されます。 RDS と呼ばれる既定のサーバー プログラムの提供、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクト。 **RDSServer.DataFactory**オブジェクトは、いずれかを返した**レコード セット**クライアントに、クエリによって生成されるオブジェクト。  
  
 ただし、 **RDSServer.DataFactory**クエリと更新プログラムの実行に制限されています。 接続またはコマンド文字列での検証または処理は実行できません。  
  
 Ado を指定できます、 **DataFactory**職場と呼ばれるサーバー プログラムの別の型と組み合わせて、*ハンドラー*します。 ハンドラーでは、データ ソースへのアクセスに使用されるようにクライアント接続とコマンド文字列を変更できます。 さらに、ハンドラーは、データ ソースにデータを読み書きするクライアントの権限を制御するアクセス権を適用できます。  
  
 ハンドラーは、クライアント パラメーターを変更して、アクセス権をで使用されるパラメーターは、カスタマイズ ファイルのセクションで指定されます。  
  
 次のトピックでは、カスタマイズの詳細について、 **DataFactory**オブジェクト。  
  
-   [カスタマイズ ファイルの概要](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [カスタマイズ ファイルの Connect セクション](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [カスタマイズ ファイルの SQL セクション](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [カスタマイズ ファイルの UserList セクション](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [カスタマイズ ファイルの Logs セクション](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [必要なクライアントの設定](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [独自のカスタム ハンドラーの記述](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


