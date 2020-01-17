---
title: RDS チュートリアル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 541c92cd34b9cbaecdd1001be29dbab8d9b194a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922412"
---
# <a name="rds-tutorial"></a>RDS チュートリアル
このチュートリアルでは、RDS のプログラミング モデルを使用して、データ ソースの更新とクエリを示しています。 最初に、このタスクの実行に必要な手順をについて説明します。 このチュートリアルは Microsoft® Visual Basic Scripting Edition (ADO の Windows Foundation Class (ADO と WFC) を備えた) で繰り返されます。  
  
 このチュートリアルは異なる言語でコーディングして 2 つの理由。  
  
-   RDS のドキュメントには、Visual Basic では、リーダーのコードが想定しています。 これにより、ドキュメントの Visual Basic プログラマにとって便利ではあってもあまり役に立ちません他の言語を使用するプログラマにとって。  
  
-   少しがわかっていて、特定の RDS 機能について不明な別の言語のあります別の言語で記述された同じ機能を探すことによって問題を解決します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="how-the-tutorial-is-presented"></a>このチュートリアルを表示する方法  
 このチュートリアルは、RDS のプログラミング モデルに基づきます。 個別にプログラミング モデルの各手順について説明します。 さらに、各ステップでは、Visual Basic のコードの一部を示しています。  
  
 コード例は、最小限のディスカッションで他の言語で繰り返されます。 指定されたプログラミング言語のチュートリアルでは、各ステップは、プログラミング モデルとチュートリアルの説明で、対応する手順でマークされます。 ステップの番号を使用して、わかりやすいチュートリアルの説明を参照してください。  
  
 RDS のプログラミング モデルは、次のセクションに記載されています。 チュートリアルを続行すると、ロードマップとして使用します。  
  
## <a name="rds-programming-model-with-objects"></a>RDS のプログラミング モデルとオブジェクト  
  
-   サーバーで、呼び出されるプログラムを指定し、クライアントから参照する方法 (プロキシ) を取得します。  
  
-   サーバー プログラムを起動します。 データ ソースおよび発行するコマンドを識別するサーバーのプログラムには、パラメーターを渡します。  
  
-   サーバーのプログラムを取得、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)ADO を使用して、通常、データ ソースからのオブジェクト。 必要に応じて、**レコード セット**オブジェクトは、サーバーで処理します。  
  
-   サーバーを返します、最終的な**レコード セット**をクライアント アプリケーションのオブジェクト。  
  
-   クライアントで、 **Recordset**オブジェクトは、必要に応じてビジュアル コントロールで簡単に使用できるフォームに配置します。  
  
-   変更、 **Recordset**オブジェクトがサーバーに送信され、データ ソースを更新するために使用します。  
  
 このチュートリアルには、次のトピックが含まれています。  
  
-   [ステップ 1: サーバー プログラム (RDS チュートリアル) を指定します。](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [手順 2:サーバーのプログラム (RDS チュートリアル) を呼び出す](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [手順 3:サーバーは、レコード セット (RDS チュートリアル) を取得します。](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [手順 4:サーバーは、レコード セット (RDS チュートリアル) を返します。](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [手順 5:DataControl が使用可能に (RDS チュートリアル)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [手順 6:変更 (RDS チュートリアル) サーバーに送信されます。](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS のチュートリアル (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>関連項目  
 [ステップ 1: サーバー プログラム (RDS チュートリアル) を指定します。](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
