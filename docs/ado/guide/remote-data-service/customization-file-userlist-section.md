---
title: カスタマイズ ファイルの UserList セクション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 558fd9c8379808e6c2f109a9c9584e8831cddd0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922767"
---
# <a name="customization-file-userlist-section"></a>カスタマイズ ファイルの UserList セクション
**Userlist**セクションに関連する、**接続**の同じセクションとセクション*識別子*パラメーター。  
  
 このセクションに含めることができます、 *ユーザー アクセス エントリ* 、アクセスを指定する、指定したユーザーの権利し、よりも優先されます、 *既定* *エントリにアクセス* の照合 **接続** セクション。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
 形式は、ユーザーのアクセス エントリです。  
  
 _userName_ **=**    
 **_accessRights_**  
  
|要素|説明|  
|----------|-----------------|  
|*userName*|*ユーザー名*のこの接続を使用しているユーザー。 有効なユーザー名が、IIS を用いて確立された**Service Manager**ダイアログ。|  
|**_accessRights_**|次のアクセス権のいずれか:<br /><br /> -   **NoAccess** -ユーザーがデータ ソースにアクセスできません。<br />-   **読み取り専用**-ユーザーがデータ ソースを読み取ることができます。<br />-   **ReadWrite** -ユーザーの読み取りまたはデータ ソースへの書き込みができます。|  
  
## <a name="see-also"></a>関連項目  
 [カスタマイズ ファイル Connect セクション](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [カスタマイズ ファイル Logs セクション](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [カスタマイズ ファイル SQL セクション](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [DataFactory のカスタマイズ](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要なクライアント設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [カスタマイズ ファイルの概要](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [独自のカスタム ハンドラーの記述](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


