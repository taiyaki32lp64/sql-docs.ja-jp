---
title: Azure Kubernetes Services (AKS) を使用して SQL Server コンテナーを配置する
description: このチュートリアルでは、Azure Kubernetes Service で Kubernetes を使用して SQL Server 高可用性ソリューションを配置する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 91607fd8a7bc7b3b104de6d0ba3e6ce97cab8137
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558351"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>Azure Kubernetes Services (AKS) を使用して Kubernetes に SQL Server コンテナーを配置する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

高可用性 (HA) のための永続ストレージを使用して、Azure Kubernetes Service (AKS) の Kubernetes で SQL Server インスタンスを構成する方法について説明します。 このソリューションでは回復性が提供されます。 SQL Server インスタンスで障害が発生した場合、Kubernetes によって新しいポッドに自動的に再作成されます。 Kubernetes では、ノード障害に対する回復性も提供されます。

このチュートリアルでは、AKS 上のコンテナーに高可用性 SQL Server インスタンスを構成する方法について説明します。

> [!div class="checklist"]
> * SA パスワードを作成する
> * ストレージを作成する
> * 配置を作成する
> * SQL Server Management Studio (SSMS) と接続する
> * 障害と復旧を検証する

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>Azure Kubernetes Service で実行されている Kubernetes 上の HA ソリューション

Kubernetes 1.6 以降では、[ストレージ クラス](https://kubernetes.io/docs/concepts/storage/storage-classes/)、[永続ボリューム要求](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)、および [Azure ディスク ボリューム タイプ](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)がサポートされています。 Kubernetes で ネイティブに SQL Server インスタンスを作成して管理できます。 この記事の例では、共有ディスクのフェールオーバー クラスター インスタンスと同様の高可用性構成を実現するために、[配置](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)を作成する方法を示します。 この構成では、Kubernetes はクラスター オーケストレーターの役割を果たします。 コンテナー内の SQL Server インスタンスで障害が発生すると、オーケストレーターにより、同じ永続ストレージに接続されるコンテナーの別のインスタンスがブートストラップされます。

![Kubernetes SQL Server クラスターの図](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

上の図で、`mssql-server` は[ポッド](https://kubernetes.io/docs/concepts/workloads/pods/pod/)内のコンテナーです。 Kubernetes により、クラスター内のリソースが調整されます。 [レプリカ セット](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)によって、ノード障害が発生した後でポッドが自動的に復旧されます。 アプリケーションがサービスに接続します。 このケースでは、サービスは、`mssql-server` の障害後も変化しない IP アドレスがホストされているロード バランサーを表します。

次の図では、`mssql-server` コンテナーで障害が発生しています。 オーケストレーターとしての Kubernetes により、レプリカ セット内に適切な数の正常なインスタンスが存在することが保証され、構成に従って新しいコンテナーが開始されます。 オーケストレーターによって同じノード上で新しいポッドを開始され、`mssql-server` によって同じ永続ストレージに再接続されます。 サービスは、再作成された `mssql-server` に接続されます。

![Kubernetes SQL Server クラスターの図](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

次の図では、`mssql-server` コンテナーがホストされているノードで障害が発生しています。 オーケストレーターによって異なるノード上で新しいポッドを開始され、`mssql-server` によって同じ永続ストレージに再接続されます。 サービスは、再作成された `mssql-server` に接続されます。

![Kubernetes SQL Server クラスターの図](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>前提条件

* **Kubernetes クラスター**
   - このチュートリアルでは、Kubernetes クラスターが必要です。 この手順では、[kubectl](https://kubernetes.io/docs/user-guide/kubectl/) を使用してクラスターを管理します。 

   - `kubectl` を使って AKS に Kubernetes クラスターを作成して接続する方法については、[Azure Container Service (AKS) クラスターのデプロイ](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster)に関する記事をご覧ください。 

   >[!NOTE]
   >ノード障害から保護するため、Kubernetes クラスターには複数のノードが必要です。

* **Azure CLI 2.0.23**
   - このチュートリアルの手順は、Azure CLI 2.0.23 に対して検証されています。

## <a name="create-an-sa-password"></a>SA パスワードを作成する

Kubernetes クラスターで SA パスワードを作成します。 Kubernetes では、パスワードなどの機密構成情報を[シークレット](https://kubernetes.io/docs/concepts/configuration/secret/)として管理できます。

次のコマンドでは、SA アカウントのパスワードが作成されます。

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   `MyC0m9l&xP@ssw0rd` は複雑なパスワードに置き換えます。

   そのコマンドを実行すると、`SA_PASSWORD` に対する値 `MyC0m9l&xP@ssw0rd` を保持する `mssql` という名前のシークレットが Kubernetes に作成されます。


## <a name="create-storage"></a>ストレージを作成する

Kubernetes クラスターで、[永続ボリューム](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)と[永続ボリューム要求](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection)を構成します。 次の手順を実行します。 

1. マニフェストを作成して、ストレージ クラスと永続ボリューム要求を定義します。  マニフェストでは、ストレージ プロビジョナー、パラメーター、[再要求ポリシー](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)を指定します。 Kubernetes クラスターでは、このマニフェストを使って、永続ストレージが作成されます。 

   次の yaml の例では、ストレージ クラスと永続ボリューム要求が定義されています。 この Kubernetes クラスターは Azure 内にあるため、ストレージ クラス プロビジョナーは `azure-disk` です。 ストレージ アカウントの種類は `Standard_LRS` です。 永続ボリューム要求は `mssql-data` という名前です。 永続ボリューム要求のメタデータには、それをストレージ クラスに接続するための注釈が含まれています。 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1beta1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   ファイルを保存します (例: **pvc.yaml**)。

1. Kubernetes で永続ボリューム要求を作成します。

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` は、ファイルを保存した場所です。

   永続ボリュームが Azure ストレージ アカウントとして自動的に作成され、永続ボリューム要求にバインドされます。 

    ![永続ボリューム要求コマンドのスクリーンショット](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. 永続ボリューム要求を確認します。

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` は、永続ボリューム要求の名前です。

   前のステップでは、永続ボリューム要求に `mssql-data` という名前が指定されています。 永続ボリューム要求に関するメタデータを表示するには、次のコマンドを実行します。

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   返されるメタデータには、`Volume` という名前の値が含まれます。 この値は、BLOB の名前にマップされます。

   ![Volume を含む、返されたメタデータのスクリーンショット](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   Volume の値は、Azure portal の次の図における BLOB の名前の一部と一致します。 

   ![Azure portal での BLOB 名のスクリーンショット](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. 永続ボリュームを確認します。

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` では、自動的に作成されて永続ボリューム要求にバインドされた永続ボリュームに関するメタデータが返されます。 

## <a name="create-the-deployment"></a>配置を作成する

この例では、SQL Server インスタンスをホストしているコンテナーが、Kubernetes 配置オブジェクトとして記述されています。 配置ではレプリカ セットが作成されます。 レプリカ セットによってポッドが作成されます。 

このステップでは、SQL Server [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) の Docker イメージに基づいてコンテナーを記述するマニフェストを作成します。 マニフェストでは、`mssql-server` 永続ボリューム要求と、Kubernetes クラスターに既に適用されている `mssql` シークレットが参照されます。 また、マニフェストでは[サービス](https://kubernetes.io/docs/concepts/services-networking/service/)についても記述されています。 このサービスはロード バランサーです。 ロード バランサーにより、SQL Server インスタンスの復旧後も IP アドレスが維持されることが保証されます。 

1. 配置を記述するマニフェスト (YAML ファイル) を作成します。 次の例では、SQL Server コンテナー イメージに基づくコンテナーを含む配置が記述されています。

   ```yaml
   apiVersion: apps/v1beta1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server:2017-latest
           ports:
           - containerPort: 1433
           env:
           - name: MSSQL_PID
             value: "Developer"
           - name: ACCEPT_EULA
             value: "Y"
           - name: MSSQL_SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   前のコードを、`sqldeployment.yaml` という名前の新しいファイルにコピーします。 次の値を更新します。 

   * MSSQL_PID `value: "Developer"`: SQL Server Developer Edition を実行するようにコンテナーを設定します。 Developer Edition には、運用データ用のライセンスは付与されません。 配置を運用環境で使用する場合は、適切なエディション (`Enterprise`、`Standard`、または `Express`) を設定します。 

      >[!NOTE]
      >詳細については、「[SQL Server のライセンス方法](https://www.microsoft.com/sql-server/sql-server-2017-pricing)」を参照してください。

   * `persistentVolumeClaim`:この値には、永続ボリューム要求に使用される名前にマップされる `claimName:` のエントリが必要です。 このチュートリアルでは `mssql-data` を使用します。 

   * `name: SA_PASSWORD`:このセクションで定義されているように、コンテナー イメージを構成して SA パスワードを設定します。

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     Kubernetes では、コンテナーを配置するときに、`mssql` という名前のシークレットを参照してパスワードの値が取得されます。 

   >[!NOTE]
   >`LoadBalancer` サービスの種類を使うことにより、SQL Server インスタンスにポート 1433 で (インターネットを経由して) リモート アクセスできるようになります。

   ファイルを保存します (例: **sqldeployment.yaml**)。

1. 配置を作成します。

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` は、ファイルを保存した場所です。

   ![配置コマンドのスクリーンショット](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   配置とサービスが作成されます。 SQL Server インスタンスはコンテナー内にあり、永続ストレージに接続されています。

   ポッドの状態を表示するには、「`kubectl get pod`」と入力します。

   ![get pod コマンドのスクリーンショット](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   上の図では、ポッドの状態は `Running` です。 この状態は、コンテナーの準備ができていることを示します。 この処理には数分かかることがあります。

   >[!NOTE]
   >配置が作成された後、ポッドが表示されるまでに数分かかることがあります。 遅延は、クラスターによって Docker Hub から [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) イメージがプルされるためです。 イメージが初めてプルされた後の配置は、既にイメージがキャッシュされているノードに対するものの場合は、高速になる可能性があります。 

1. サービスが実行されていることを確認します。 次のコマンドを実行します。

   ```azurecli
   kubectl get services 
   ```

   このコマンドでは、実行されているサービスと共に、サービスの内部および外部の IP アドレスも返されます。 `mssql-deployment` サービスの外部 IP アドレスを記録しておきます。 この IP アドレスを使って SQL Server に接続します。 

   ![get service コマンドのスクリーンショット](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Kubernetes クラスター内のオブジェクトの状態に関する詳細情報を取得するには、以下を実行します。

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>SQL Server インスタンスに接続する

説明に従ってコンテナーを構成した場合は、Azure 仮想ネットワークの外部からアプリケーションに接続できます。 `sa` アカウントと、サービスの外部 IP アドレスを使います。 Kubernetes シークレットとして構成したパスワードを使います。 

次のアプリケーションを使って、SQL Server インスタンスに接続できます。 

* [SSMS](https://docs.microsoft.com/sql/linux/sql-server-linux-manage-ssms)

* [SSDT](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   `sqlcmd` を使って接続するには、次のコマンドを実行します。

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   次の値を置き換えます。
      
    - `<External IP Address>` は、`mssql-deployment` サービスの IP アドレスに 
    - `MyC0m9l&xP@ssw0rd` は、自分のパスワードに

## <a name="verify-failure-and-recovery"></a>障害と復旧を検証する

障害と復旧を確認するには、ポッドを削除します。 手順は次のとおりです。

1. SQL Server が実行されているポッドの一覧を表示します。

   ```azurecli
   kubectl get pods
   ```

   SQL Server が実行されているポッドの名前を記録します。

1. ポッドを削除します。

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` は、前のステップでポッド名に対して返された値です。 

Kubernetes では、ポッドが自動的に再作成されて SQL Server インスタンスが復旧され、永続ストレージに接続されます。 新しいポッドが配置されたことを確認するには、`kubectl get pods` を使います。 新しいコンテナーの IP アドレスが同じであることを確認するには、`kubectl get services` を使います。 

## <a name="summary"></a>まとめ

このチュートリアルでは、高可用性を実現するために SQL Server コンテナーを Kubernetes クラスターに配置する方法を学習しました。 

> [!div class="checklist"]
> * SA パスワードを作成する
> * ストレージを作成する
> * 配置を作成する
> * SQL Server Management Studio (SSMS) と接続する
> * 障害と復旧を検証する

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
>[Kubernetes の概要](https://docs.microsoft.com/azure/aks/intro-kubernetes)


