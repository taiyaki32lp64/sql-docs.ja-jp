---
title: 基本的な RDS のプログラミング モデル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84b90e2c1338c38538d0c33779fb8e3f5cf2af79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922954"
---
# <a name="basic-rds-programming-model"></a>RDS の基本プログラミング モデル
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 Rds は、次の環境に存在するアプリケーション。クライアント アプリケーションでは、サーバーおよび必要な情報を返すために必要なパラメーターで実行するプログラムを指定します。 指定されたデータ ソースへのサーバーがアクセスに対して呼び出されたプログラム情報を取得するには、必要に応じて、データを処理および簡単に使用できる形式でクライアント アプリケーションに、結果の情報を返します。 RDS は、次の一連のアクションを実行するための手段を提供します。  
  
-   サーバーで、呼び出されるプログラムを指定し、クライアントからそれを参照する方法を取得します。 (この参照が呼び出される場合があります、*プロキシ*します。 リモート サーバーのプログラムを表します。 クライアント アプリケーションは"call"のプロキシと場合、ローカルのプログラムが実際には、リモート サーバーのプログラムを呼び出します。)  
  
-   サーバー プログラムを起動します。 データ ソースおよび発行するコマンドを識別するサーバーのプログラムには、パラメーターを渡します。 (サーバー プログラム実際には ADO を使用して、データ ソースにアクセスできます。 ADO、特定のパラメーターのいずれかの接続を確立し、他のパラメーターで指定されたコマンドを発行します。)  
  
-   サーバーのプログラムを取得、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)データ ソースからのオブジェクト。 必要に応じて、**レコード セット**オブジェクトは、サーバーで処理します。  
  
-   サーバーを返します、最終的な**レコード セット**をクライアント アプリケーションのオブジェクト。  
  
-   クライアントで、**レコード セット**ビジュアル コントロールで簡単に使用できる形式にオブジェクトを配置します。  
  
-   変更したり、 **Recordset**オブジェクトがそれらを使用して、データ ソースを更新するサーバーのプログラムに送信されます。  
  
 このプログラミング モデルには、特定の便利な機能が含まれています。 RDS が自動的には、必要な接続とコマンド パラメーターを指定する場合、データ ソースにアクセスする複雑なサーバー プログラムを必要としない場合は、単純で、既定のサーバーのプログラムで指定されたデータを取得します。  
  
 複雑な処理が必要な場合は、独自のカスタム サーバー プログラムを指定できます。 たとえば、カスタム サーバー プログラムには、破棄された時点の ADO の全機能があるため、いくつかの異なるデータ ソースに接続、何らかの複雑な方法でそのデータを組み合わせる、クライアント アプリケーションに処理され、単純な結果を返すおよびでした。  
  
 最後に場合は、ニーズの場所間に、ADO サポート既定のサーバー プログラムの動作をカスタマイズします。  
  
## <a name="see-also"></a>関連項目  
 [RDS のプログラミング モデルの詳細](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS のシナリオ](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS チュートリアル](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS の使用方法とセキュリティ](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


