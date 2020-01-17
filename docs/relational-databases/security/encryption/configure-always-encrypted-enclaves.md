---
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を構成して使用する | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 568944db62ca94048c45450500d3060daa957680
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317940"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を構成して使用する 

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) は、既存の [Always Encrypted ](always-encrypted-database-engine.md) 機能を拡張して、データを機密性に保ちながら機密データに対してより高度な機能を有効にすることができます。 この記事では、この機能を構成して使用するための一般的なタスクを示します。

セキュリティで保護されたエンクレーブが設定された Always Encrypted をすぐに使い始める方法がわかるチュートリアルについては、「[チュートリアル: Getting started with Always Encrypted with secure enclaves using SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)」 (チュートリアル: SSMS を使用するセキュリティで保護されたエンクレーブが設定された Always Encrypted の概要) を参照してください。

## <a name="set-up-your-environment-to-support-enclaves-and-attestation"></a>エンクレーブと構成証明をサポートする環境を設定する
詳しくは、次の記事を参照してください。
- [ホスト ガーディアン サービスの構成証明の計画](./always-encrypted-enclaves-host-guardian-service-plan.md)
- [[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] のホスト ガーディアン サービスを配置する](./always-encrypted-enclaves-host-guardian-service-deploy.md)
- [ホスト ガーディアン サービスにコンピューターを登録する](./always-encrypted-enclaves-host-guardian-service-register.md)

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する - 概要](always-encrypted-enclaves-manage-keys.md)
- [エンクレーブ対応キーをプロビジョニングする](always-encrypted-enclaves-provision-keys.md)
- [エンクレーブ対応キーをローテーションする](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted で列を構成する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する - 概要](always-encrypted-enclaves-configure-encryption.md)
- [Transact-SQL を使用してインプレースでの列の暗号化を構成する](always-encrypted-enclaves-configure-encryption-tsql.md)
- [既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする](always-encrypted-enclaves-enable-for-encrypted-columns.md)

> [!NOTE]
> テスト環境を設定し、SSMS でセキュリティで保護されたエンクレーブが設定された Always Encrypted の機能を試す方法の手順を説明したチュートリアルについては、「[Tutorial: Getting started with Always Encrypted with secure enclaves using SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)」 (チュートリアル: SSMS を使用するセキュリティで保護されたエンクレーブが設定された Always Encrypted の概要) を参照してください。

## <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを実行する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを実行する - 概要](always-encrypted-enclaves-query-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを SSMS で実行する](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>エンクレーブ対応の列でインデックスを作成して使用する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブ列が設定された Always Encrypted でのインデックスの作成と使用](always-encrypted-enclaves-create-use-indexes.md)

## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する
詳しくは、以下の記事を参照してください。
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)
