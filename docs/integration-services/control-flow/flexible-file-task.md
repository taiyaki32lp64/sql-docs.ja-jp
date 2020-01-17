---
title: 柔軟なファイル タスク | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4ed8ba34e8e50d6414d68cae4aa386848f88b6d5
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72807412"
---
# <a name="flexible-file-task"></a>柔軟なファイル タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

柔軟なファイル タスクにより、サポートされているさまざまなストレージ サービスでファイル操作を実行できるようになります。
現在サポートされているストレージ サービスは次のとおりです。

- ローカル ファイル システム
- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

柔軟なファイル タスクは、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。

パッケージに柔軟なファイル タスクを追加するには、SSIS ツールボックスからデザイナー キャンバスにドラッグします。 次に、タスクをダブルクリックするか、右クリックして **[編集]** を選択し、 **[Flexible File Task Editor]\(柔軟なファイル タスク エディター\)** ダイアログ ボックスを開きます。

**[操作]** プロパティでは、実行するファイル操作を指定します。
現在サポートされている操作は、次のとおりです。
- **コピー**操作
- **削除**操作

**コピー**操作に対して使用できるプロパティは次のとおりです。

- **SourceConnectionType:** ソース接続マネージャーの種類を指定します。
- **SourceConnection:** ソース接続マネージャーを指定します。
- **SourceFolderPath:** ソース フォルダーのパスを指定します。
- **SourceFileName:** ソース ファイル名を指定します。 空白のままにすると、ソース フォルダーがコピーされます。
- **SearchRecursively:** サブフォルダーを再帰的にコピーするかどうかを指定します。
- **DestinationConnectionType:** 送信先接続マネージャーの種類を指定します。
- **DestinationConnection:** 送信先接続マネージャーを指定します。
- **DestinationFolderPath:** 送信先フォルダーのパスを指定します。
- **DestinationFileName:** 送信先ファイル名を指定します。

**削除**操作に対して使用できるプロパティは次のとおりです。
- **ConnectionType:** 接続マネージャーの種類を指定します。
- **Connection:** 接続マネージャーを指定します。
- **FolderPath:** フォルダーのパスを指定します。
- **FileName:** ファイル名を指定します。 空白のままにすると、フォルダーが削除されます。 Azure Blob Storage の場合、フォルダーの削除はサポートされていません。

***サービス プリンシパルのアクセス許可の構成に関する注意事項***

**テスト接続**が機能するためには (BLOB ストレージまたは Data Lake Storage Gen2)、サービス プリンシパルには少なくともストレージ アカウントに対する**ストレージ BLOB データ閲覧者**の役割を割り当てる必要があります。
これは、[RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) を使用して行います。

BLOB ストレージの場合、少なくとも**ストレージ BLOB データ閲覧者**と**ストレージ BLOB データ共同作成者**の役割をそれぞれ割り当てることにより、読み取りと書き込みのアクセス許可が付与されます。

Data Lake Storage Gen2 の場合、アクセス許可は RBAC と [ACL](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer) の両方によって決定されます。
[こちら](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal)に説明されているように、アプリ登録に対応するサービス プリンシパルのオブジェクト ID (OID) を使用して ACL を構成することに注意してください。
これは、RBAC 構成で使用されるアプリケーション (クライアント) ID とは異なります。
組み込みロールまたはカスタム ロールを使用してセキュリティ プリンシパルに RBAC データ アクセス許可が付与されると、これらのアクセス許可は、要求の認可時に最初に評価されます。
要求された操作がセキュリティ プリンシパルの RBAC 割り当てによって認可された場合、認可はすぐに解決され、追加の ACL チェックは実行されません。
また、セキュリティ プリンシパルに RBAC 割り当てがない場合、または要求の操作が割り当てられたアクセス許可と一致しない場合、ACL チェックが実行され、要求された操作を実行する権限がセキュリティ プリンシパルに付与されているかどうかが判断されます。

- 読み取りアクセス許可の場合、少なくともソース ファイル システムから開始する**実行**アクセス許可を、コピーするファイルに対する**読み取り**アクセス許可と共に付与します。 または、少なくとも**ストレージ BLOB データ閲覧者**の役割を RBAC を使用して付与します。
- 書き込みアクセス許可の場合、少なくともシンク ファイル システムから開始する**実行**アクセス許可を、シンク フォルダーに対する**書き込み**アクセス許可と共に付与します。 または、少なくとも**ストレージ BLOB データ共同作成者**の役割を RBAC を使用して付与します。

詳細については、[この記事](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control)を参照してください。
