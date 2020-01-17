---
title: DCOM Stream の形式のマーシャ リングの設定 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29bf8d19b9e3c9ec9b4072edd9575add9947c8f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922217"
---
# <a name="setting-dcom-stream-marshaling-format"></a>DCOM のストリームのマーシャリング形式の設定
RDS 1.5 以前のコンポーネントを使用してクライアント コンピューターは、RDS 2.0 またはそれ以降のコンポーネントを使用するサーバーと互換性がありません。 RDS 2.0 またはそれ以降のサポートはより効率的に転送を基になるプロトコルとして DCOM を使用する場合[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 RDS 1.5 以前のコンポーネント、クライアントを実行する場合は、(RDS 1.0 と呼ばれます) 前の RDS サポートや新しい RDS サポート (2.0 以降と呼ばれる RDS) を使用するようにサーバーを設定できます。 次のレジストリ エントリのいずれかを設定します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 \- または -  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


