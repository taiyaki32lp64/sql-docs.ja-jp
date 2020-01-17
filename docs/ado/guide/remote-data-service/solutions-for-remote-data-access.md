---
title: リモート データ アクセスのソリューション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 40485562c8385e05ced033062563d5c5165218de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922176"
---
# <a name="solutions-for-remote-data-access"></a>リモート データ アクセスのソリューション
## <a name="the-issue"></a>問題  
 ADO を使用すると、アプリケーションに直接アクセスして (2 層システムとも呼ばれます) のデータ ソースを変更します。 たとえば、データを含むデータ ソースに接続する場合は、内にある直接接続 2 層システムです。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 ただし、Microsoft® インターネット インフォメーション サービス (IIS) などの中間層を通じてしないデータ ソースに直接アクセスしたい場合があります。 この配置は、3 層システムと呼ばれます。 IIS は、ローカル、またはクライアントをインターネットまたはイントラネットの間で、リモートまたはサーバー、プログラムを起動するアプリケーションの効率的な方法を提供するクライアント/サーバー システムです。 サーバーのプログラムでは、データ ソースにアクセスし、必要に応じて取得したデータを処理します。  
  
 たとえば、イントラネットの Web ページには、Microsoft® Visual Basic Scripting Edition (VBScript) を IIS に接続するで記述されたアプリケーションが含まれています。 IIS で、実際のデータ ソースに接続、データを取得、何らかの方法で処理、およびアプリケーションに処理された情報を返します。  
  
 この例で、アプリケーションは直接接続されているデータ ソースにIIS は次のとおりでした。 IIS ADO を使用してデータにアクセスします。  
  
> [!NOTE]
>  クライアント/サーバー アプリケーションは、インターネットまたはイントラネットに基づいて作成する必要はありません (つまり、Web ベース)-ローカル エリア ネットワーク上のコンパイル済みプログラムのためだけで構成されている可能性があります。 ただし、一般的なケースは、Web ベースのアプリケーションです。  
  
 グリッド、チェック ボックスをオンまたは ボックスの一覧など、いくつかのビジュアル コントロールは、返される情報を使用しても、ため、ビジュアルなコントロールによって返される情報を簡単に使用する必要があります。  
  
 シンプルで効率的なアプリケーション プログラミング インターフェイスを 3 層システムをサポートし、に関する情報を返しますとして簡単に取得されていた場合、2 層システムを必要とします。 リモート データ サービス (RDS) は、このインターフェイスです。  
  
## <a name="the-solution"></a>解決策  
 RDS では、一連のアクティビティにアクセスし、インターネット インフォメーション サービス (IIS) など、仲介者を使用してデータにアクセスする - データ ソースを更新するために必要なプログラミング モデルを定義します。 プログラミング モデルは、RDS の全体の機能をまとめたものです。  
  
## <a name="see-also"></a>関連項目  
 [基本的な RDS のプログラミング モデル](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS のシナリオ](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS チュートリアル](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS の使用方法とセキュリティ](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


