---
title: ビジネス オブジェクトのスクリプトに対して安全としてマーク |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55ae560f35a06e77803bfb011f4d430d5079ea05
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922602"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>スクリプト用にビジネス オブジェクトを安全とマークする
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 インターネット環境のセキュリティを確保するにはでインスタンス化されたビジネス オブジェクトをマークする必要があります、 [rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)オブジェクトの[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)メソッドとして「スクリプトの安全な」。 ようにマークされていると、システム レジストリのライセンスの領域に dcom を使用することを確認する必要があります。  
  
> [!NOTE]
>  「安全」にスクリプトまたは初期化に対して安全としてマークされているビジネス オブジェクトをインスタンス化し、ネットワーク経由ですべてのユーザーによって初期化されることができます。 「スクリプトの安全な」ビジネス オブジェクトをマークすることはありません、セーフ。 ビジネス オブジェクトがこのようなオブジェクトは、機密データの保護されていないアクセス ポイントを存在しないことを確認します。 最高のセキュリティとコード化されたかどうかを確認する非常に重要ですが。  
  
 スクリプトを実行しても安全だとビジネス オブジェクトを手動でマークするには、次のテキストを含む .reg という拡張子でテキスト ファイルを作成します。 この例で\< *MyActiveXGUID*> ビジネス オブジェクトの 16 進数の GUID の数です。 次の 2 つの数値は、safe-スクリプトの機能を有効にします。  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 ファイルを保存し、レジストリ エディターを使用するか、Windows エクスプ ローラーで、.reg ファイルをダブルクリックすると、レジストリにマージします。  
  
 Microsoft Visual Basic で作成されたビジネス オブジェクトは、パッケージおよび展開ウィザードを使用「スクリプトの安全な」として自動的にマークすることができます。 ウィザードでは、安全性の設定を指定することが表示されたら、選択**初期化に対して安全**と**スクリプトにとって安全だ**します。  
  
 最後の手順では、アプリケーションのセットアップ ウィザードは .htm ファイル、.cab ファイルを作成します。 対象のコンピュータにこれら 2 つのファイルをコピーし、ページを読み込むし、サーバーを正しく登録するには、.htm ファイルをダブルクリックしています。  
  
 ビジネス オブジェクトは、既定では、Windows\System32\Occache ディレクトリにインストールされる、ため windows \system32 ディレクトリに移動し、変更、 **hkey_classes_root \clsid\\**  \< *MyActiveXGUID*>\\**InprocServer32**レジストリ キーに正しいパスと一致します。


