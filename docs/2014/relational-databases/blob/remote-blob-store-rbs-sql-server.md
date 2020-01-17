---
title: リモート BLOB ストア (RBS) [SQL Server] | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Remote Blob Store (RBS) [SQL Server]
- RBS (Remote Blob Store) [SQL Server]
ms.assetid: 31c947cf-53e9-4ff4-939b-4c1d034ea5b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4379e0ff3ca534acd6ae130cbdf0f8acd2b6a81f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66009847"
---
# <a name="remote-blob-store-rbs-sql-server"></a>リモート BLOB ストア (RBS) [SQL Server]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリモート BLOB ストア (RBS) はオプションのアドオン コンポーネントです。これを使用すると、データベース管理者は、バイナリ ラージ オブジェクトを、主なデータベース サーバーに直接格納するのではなく、汎用的なストレージ ソリューションに格納できます。  
  
 RBS は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール メディアに含まれていますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ プログラムではインストールされません。  
  
 RBS の詳細については、このトピックの「 [RBS リソース](#rbsresources) 」を参照してください。  
  
## <a name="benefits-of-rbs"></a>RBS の利点  
 RBS には、次の利点があります。  
  
### <a name="optimized-database-storage-and-performance"></a>最適化されたデータベース ストレージとパフォーマンス  
 BLOB をデータベースに格納する場合は、大量のファイル領域と高コストのサーバー リソースが消費されることがあります。 RBS は、BLOB を選択した専用ストレージ ソリューションに効率的に転送し、データベースにその参照を格納します。 これにより、構造化データ用のサーバー ストレージが解放され、データベース操作用のサーバー リソースが解放されます。  
  
### <a name="efficient-management-of-blobs"></a>BLOB の効率的な管理  
 複数の RBS 機能では、格納された BLOB を容易に管理できます。  
  
-   BLOB は、ACID (原子性、一貫性、分離性、持続性) を備えたトランザクションで管理します。  
  
-   BLOB は、いくつかのコレクションで構成されています。  
  
-   ガベージ コレクション、一貫性チェック、およびその他のメンテナンス機能が含まれています。  
  
### <a name="standardized-api"></a>標準化された API  
 RBS では、アプリケーションから BLOB ストアにアクセスして変更するための標準化されたプログラミング モデルを提供する一連の API が定義されています。 各 BLOB ストアでは、独自のプロバイダー ライブラリを指定できます。このライブラリは、RBS クライアント ライブラリに接続して、BLOB の格納方法やアクセス方法を指定します。  
  
 多数のサード パーティのストレージ ソリューション ベンダーが、これらの標準 API に準拠し、さまざまなストレージ プラットフォームで BLOB ストレージをサポートする RBS プロバイダーを開発しています。  
  
## <a name="rbs-requirements"></a>RBS 要件  
 RBS では、BLOB メタデータが格納されている主なデータベース サーバー用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise が必要です。 ただし、指定された FILESTREAM プロバイダーを使用する場合は、BLOB 自体を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard に格納できます。  
  
 RBS には、RBS を使用して BLOB を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで格納できる FILESTREAM プロバイダーが含まれています。 RBS を使用して BLOB を別のストレージ ソリューションに格納する場合は、そのストレージ ソリューション用に開発されたサード パーティの RBS プロバイダーを使用するか、RBS API を使用してカスタム RBS プロバイダーを開発する必要があります。 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190)には、NTFS ファイル システムに BLOB を格納するサンプル プロバイダーが学習用リソースとして用意されています。  
  
## <a name="rbs-security"></a>RBS セキュリティ  
 カスタム プロバイダーを使用して BLOB を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の外部に格納する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ システムをバイパスするその他のプロセスで使用される場合があります。 カスタム プロバイダーが使用するストレージ メディアに適した権限と暗号化オプションで格納された BLOB が保護されていることを確認してください。  
  
##  <a name="rbsresources"></a> RBS リソース  
 **RBS ドキュメント**  
 RBS ドキュメントは Windows インストーラー パッケージに含まれています。 RBS をインストールせずに RBS ドキュメントを確認する場合は、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版のドキュメントを [MSDN ライブラリからオンライン](https://go.microsoft.com/fwlink/?LinkId=210192)で参照できます。  
  
 **RBS ホワイト ペーパー**  
 Microsoft Word 文書としてダウンロードできるホワイト ペーパー「[リモート BLOB ストレージ](https://go.microsoft.com/fwlink/?LinkId=210422)」には、RBS のインストールと構成の詳細が記載されています。  
  
 **RBS サンプル**  
 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190) で入手できる RBS サンプルでは、RBS アプリケーションの開発方法とカスタム RBS プロバイダーの開発およびインストール方法を示します。  
  
 **RBS ブログ**  
 [RBS ブログ](https://go.microsoft.com/fwlink/?LinkId=210315) には、RBS の理解、配置、および維持に役立つ追加情報が含まれています。  
  
  
