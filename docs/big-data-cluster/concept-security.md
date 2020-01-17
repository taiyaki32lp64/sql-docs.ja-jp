---
title: セキュリティの概念
titleSuffix: SQL Server big data clusters
description: この記事では、SQL Server ビッグ データ クラスターのセキュリティの概念について説明します。 これには、クラスター エンドポイントとクラスター認証の説明が含まれます。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 35eb5e0a3236d8f016ed5ca99b769d628a4d81ed
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532379"
---
# <a name="security-concepts-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]のセキュリティの概念

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、ビッグ データ クラスターのセキュリティに関する重要な概念について説明します

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]では、明確で一貫性のある承認と認証が提供されます。 ビッグ データ クラスターは、既存のドメインに対して Active Directory 統合をセットアップする完全に自動化された展開を通じて、Active Directory と統合できます。 Active Directory 統合を使用してビッグ データ クラスターを構成すると、既存の ID とユーザー グループを活用して、すべてのエンドポイントにわたる統合アクセスを実現できます。 また、SQL Server 内で外部テーブルを作成した後は、外部テーブルへのアクセスを Active Directory ユーザーとグループに許可することで、データ ソースへのアクセスを制御できます。これにより、データ アクセス ポリシーが 1 か所に一元化されます。

## <a name="authentication"></a>認証

外部クラスター エンドポイントでは、Active Directory 認証がサポートされます。 これは、AD ID を使用してビッグ データ クラスターを認証できることを意味します。

### <a name="cluster-endpoints"></a>クラスター エンドポイント

ビッグ データ クラスターには 5 つのエントリ ポイントがあります

* マスター インスタンス - SSMS や Azure Data Studio など、データベース ツールとアプリケーションを使用してクラスター内の SQL Server マスター インスタンスにアクセスするための TDS エンドポイント。 azdata から HDFS または SQL Server コマンドを使用する場合、操作に応じて、ツールは他のエンドポイントに接続します。

* HDFS ファイル、Spark (Knox) にアクセスするためのゲートウェイ - これは HTTPS ベースのエンドポイントです。 このエンドポイントは、webHDFS や Spark などのサービスにアクセスするために使用されます。

* クラスター管理サービス (コントローラー) エンドポイント - クラスターを管理するための REST API を公開しているビッグ データ クラスター管理サービスです。 Azdata ツールは、このエンドポイントに接続する必要があります。

* 管理プロキシ - ログ検索ダッシュボードとメトリック ダッシュボードにアクセスするために使用します。

* アプリケーション プロキシ - ビッグ データ クラスター内に展開されたアプリケーションを管理するためのエンドポイント。

![クラスター エンドポイント](media/concept-security/cluster_endpoints.png)

現時点では、外部からクラスターにアクセスするための追加のポートを開くオプションはありません。

## <a name="authorization"></a>承認

クラスター全体を通じて、さまざまなコンポーネント間の統合セキュリティにより、Spark や SQL Server からクエリを発行するときに元のユーザーの ID を HDFS に渡すことができます。 前述のように、さまざまな外部クラスター エンドポイントで AD 認証がサポートされています。

クラスターには、データ アクセスを管理するための 2 レベルの承認チェックがあります。 ビッグ データのコンテキストでの承認は、オブジェクトに対する従来の SQL Server アクセス許可を使用して SQL Server 内で、また、ユーザー ID を特定のアクセス許可に関連付ける制御リスト (ACL) を使用して HDFS 内で行われます。

セキュリティで保護されたビッグ データ クラスターとは、SQL Server と HDFS/Spark の両方にまたがる、認証と承認のシナリオに対する一貫性のあるわかりやすいサポートを意味します。 認証とは、ユーザーまたはサービスの身元を確認し、ユーザーまたはサービスが本物であることを確認するプロセスです。 承認とは、要求元のユーザーの ID に基づいて、特定のリソースへのアクセスを許可または拒否することを意味します。 この手順は、ユーザーが認証によって識別された後に実行されます。

通常、ビッグ データのコンテキストにおける承認は、ユーザー ID と特定のアクセス許可を関連付けるアクセス制御リスト (ACL) を使用して実行されます。 HDFS は、サービス API、HDFS ファイル、およびジョブ実行に対するアクセスを制限することで、承認をサポートするものです。

## <a name="encryption-and-other-security-mechanisms"></a>暗号化およびその他のセキュリティ メカニズム

クライアントと外部エンドポイント間およびクラスター内のコンポーネント間の通信の暗号化は、証明書を使用して TLS/SSL で保護されます。

データ プールと通信する SQL マスター インスタンスなど、SQL Server 間のすべての通信は、SQL ログインを使用して保護されます。

## <a name="basic-administrator-login"></a>基本管理者ログイン

クラスターを Active Directory モードで展開するか、基本管理者ログインのみを使用して展開するかを選択できます。 基本管理者ログインのみを使用することは、運用環境でサポートされているセキュリティ モードではなく、主に製品の評価を目的としています。

Active Directory モードを選択した場合でも、クラスター管理者に対して基本ログインが作成されます。 これにより、AD 接続が停止した場合の "バックドア" が提供されます。

展開時に、この基本ログインにはクラスター内での管理者権限が付与されます。 これは、ユーザーが SQL Server マスター インスタンス内のシステム管理者となり、クラスター コントローラー内の管理者となることを意味します。
Hadoop コンポーネントでは混合モード認証がサポートされません。つまり、基本管理者ログインを使用してゲートウェイ (knox) に対する認証を行うことはできません。


これらは、展開時に定義する必要があるログイン資格情報です。

クラスター管理者のユーザー名:
 + `AZDATA_USERNAME=<username>`

クラスター管理者のパスワード:  
 + `AZDATA_PASSWORD=<password>`

> [!NOTE]
> 非 AD モードでは、HDFS/Spark にアクセスするためにゲートウェイ (Knox) に対して認証を行うために、ユーザー名 "root" を上記のパスワードと組み合わせて使用する必要があることに注意してください。

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] の詳細については、次のリソースを参照してください。

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)
- [ワークショップ: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] アーキテクチャ](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
