---
title: "バイナリ ラージ オブジェクト (Blob) データ (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4a9291aa99091d1b44e4b829af803637250bd333
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="binary-large-object-blob-data-sql-server"></a>バイナリ ラージ オブジェクト (Blob) データ (SQLServer)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、ファイルおよびドキュメントをデータベースまたはリモート ストレージ デバイスに格納するためのソリューションが用意されています。  
  
##  <a name="section"></a> このセクションの内容  
 [BLOB の保存オプションの比較 &#40;SQL Server&#41;](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md)  
 FILESTREAM、FileTable、およびリモート BLOB ストアの利点を比較します。  
  
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
 FILESTREAM を使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ベースのアプリケーションで非構造化データ (ドキュメントやイメージなど) をファイル システムに格納できます。 これにより、ファイル システムの豊富なストリーミング API と高いパフォーマンスをアプリケーションで活用できるほか、非構造化データとそれに対応する構造化データの間でトランザクションの一貫性も維持されます。  
  
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
 FileTable 機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されているファイル データに対して Windows ファイル名前空間のサポートと Windows アプリケーションとの互換性を提供します。 FileTable により、アプリケーションは、ストレージとデータ管理コンポーネントを統合し、非構造化データおよびメタデータに対する統合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス (フルテキスト検索、セマンティック検索など) を提供できます。  
  
 つまり、ファイルおよびドキュメントを FileTable と呼ばれる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特殊なテーブルに保存しておき、ファイル システムに格納されているかのように、Windows アプリケーションからこれらのファイルおよびドキュメントにアクセスできるということです。このとき、クライアント アプリケーションに変更を加える必要はありません。  
  
 [リモート BLOB ストア &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリモート BLOB ストア (RBS) を使用すると、データベース管理者は、バイナリ ラージ オブジェクト (BLOB) を、直接サーバーに格納するのではなく、汎用的なストレージ ソリューションに格納できます。 これにより、容量を大幅に節約でき、コストのかかるサーバー ハードウェア リソースの浪費を回避できます。 RBS では、アプリケーションが BLOB データにアクセスするための標準化されたモデルを定義する一連の API ライブラリが提供されます。 また、RBS には、リモート BLOB データの管理に役立つメンテナンス ツール (ガベージ コレクションなど) も用意されています。  
  
 RBS は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール メディアに含まれていますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ プログラムではインストールされません。  
  
  