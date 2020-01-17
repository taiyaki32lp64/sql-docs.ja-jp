---
title: コンポーネント サービスでビジネス オブジェクトの実行 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87eab0ac5611b437f6e0cbe1957a4d6e8652c4b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922279"
---
# <a name="running-business-objects-in-component-services"></a>コンポーネント サービスでのビジネス オブジェクトの実行
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 ビジネス オブジェクトには、実行可能ファイル (.exe) またはダイナミック リンク ライブラリ (.dll) を指定できます。 構成を使用して、ビジネス オブジェクトを実行するかどうか、オブジェクトは、.dll または .exe ファイルによって異なります。  
  
-   .Exe ファイルとして作成されたビジネス オブジェクトは、DCOM を介して呼び出すことができます。 クライアントのパフォーマンスが低下する、データの追加のマーシャ リングされるインターネット インフォメーション サービス (IIS) を介してこれらのビジネス オブジェクトを使用する場合。  
  
-   As .dll ファイルを使用して、IIS を介して作成されたビジネス オブジェクトと HTTP でも。 いることもできます、コンポーネント サービスを介してのみまたは Microsoft Transaction Server では、DCOM 経由で Windows NT を使用している場合。 ビジネス オブジェクトの Dll は、IIS を介してそれらにアクセスする IIS サーバー コンピューターに登録する必要があります。 DCOM 上で実行する DLL を構成する方法については、このセクションを参照してください。 [DCOM 上で実行するように DLL を有効にする](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md)します。  
  
> [!NOTE]
>  使用して、中間層ビジネス オブジェクトがコンポーネント サービス コンポーネントとして実装すると**GetObjectContext**、 **SetComplete**、および**SetAbort**、ビジネスオブジェクトは、コンポーネント サービス (または Windows NT を使用している場合は、MTS) を使用できる複数のクライアント呼び出しでその状態を維持するために、コンテキスト オブジェクト。 このシナリオでは、DCOM で、信頼されたクライアントとイントラネット内のサーバーの間は、通常実装を持つ可能性があります。 ここで、 [rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)オブジェクトと[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)クライアント側のメソッドは、トランザクションのコンテキスト オブジェクトに置き換え、 **CreateInstance** によって提供されるメソッドは、**ITransactionContext**インターフェイスし、コンポーネント サービスによって実装されます。  
  
## <a name="see-also"></a>関連項目  
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)


