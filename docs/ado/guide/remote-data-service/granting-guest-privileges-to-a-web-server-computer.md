---
title: Web サーバーのコンピューターへのゲスト特権の付与 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bddf6ce0bbfb78435118ef3d87303a94c792c96d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922643"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>Web サーバー コンピューターへのゲスト特権の付与
匿名の Web サーバーのアカウント (iusr _*ComputerName*) RDS を使用して、ゲストをローカル Web サーバー コンピューターのグループに追加する必要があります  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>Web サーバー コンピューターへのゲスト特権を付与するには  
  
1.  Microsoft Windows 2000 Server コンピューターに次のようにクリックします**開始**、 をポイント**プログラム**、 をポイント**管理ツール**、 をクリックし、**コンピューター。管理**します。  
  
2.  コンソール ツリーで [**ローカル ユーザーとグループ**、] をクリックして**グループ**します。  
  
3.  選択、**ゲスト**ローカル グループです。 **アクション**] メニューの [選択**プロパティ**します。  
  
4.  **ゲスト プロパティ**ダイアログ ボックスで、をクリックして**追加**します。  
  
5.  一覧で、匿名の Web サーバーのアカウントが表示されないかどうか、 **ユーザーまたはグループ** ダイアログ ボックスで、その名前を入力 (iusr _*ComputerName*) をクリックし、下部にある空白ボックスに**追加**.  
  
6.  **[OK]** をクリックします。


