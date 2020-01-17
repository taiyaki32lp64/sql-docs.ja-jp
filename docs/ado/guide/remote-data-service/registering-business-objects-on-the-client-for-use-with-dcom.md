---
title: DCOM を使用するためのクライアントでビジネス オブジェクトに登録 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31af4a68ec830a5fd514173c831ce3863fef7443
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922354"
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>DCOM で使用するためにクライアントにビジネス オブジェクトを登録する
カスタム ビジネス オブジェクトは、クライアント側が DCOM 経由で使用できる識別子 (CLSID) に、プログラム名 (ProgId) をマップできることを確認する必要があります。 このため、DCOM オブジェクトの ProgID はクライアント側のレジストリにし、サーバー側ビジネス オブジェクトのクラス ID にマップする必要があります。 その他のサポートされているプロトコル (HTTP、HTTPS、およびプロセス内)、これは必要ありません。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 たとえば、特定のクラス ID、たとえば、"{00112233-4455-6677-8899-00AABBCCDDEE}"mybobj サーバー側ビジネス オブジェクトを公開する場合確認、次のエントリは、クライアント側のレジストリに追加されます。  
  
```console
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


