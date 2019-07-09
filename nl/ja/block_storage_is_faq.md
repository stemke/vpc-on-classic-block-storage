---

copyright:
  years: 2019
lastupdated: "2019-06-17"

keywords: block storage, IBM Cloud, VPC, virtual private cloud, boot volume, data volume, volume, data storage, virtual server instance, instance, IOPS

subcollection: vpc-on-classic-block-storage

---
{:faq: data-hd-content-type='faq'}
{:codeblock: .codeblock}
{:screen: .screen}

# Block Storage for VPC のよくある質問
{: #block-storage-vpc-faq}

## インスタンスにストレージを割り振るには、どのようにすればよいですか?
{: faq}

仮想サーバー・インスタンスを作成するときに、そのインスタンスに接続する[ブロック・ストレージ・ボリュームを作成](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-creating-block-storage#create-from-vsi)できます。また、[スタンドアロン・ボリュームを作成](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-creating-block-storage#create-standalone-vol)して、後でそれらをインスタンスに接続することもできます。

## プロビジョンされたブロック・ストレージ・ボリュームを共有できるインスタンスの数はいくつですか?
{: faq}

ブロック・ストレージ・ボリュームは、一度に 1 つのインスタンスにしか接続できません。インスタンスは同じボリュームを共有できません。

## 1 つのインスタンスに接続できるブロック・ストレージ 2 次 (データ) ボリュームの数はいくつですか?
{: faq}

vCPU が 4 つ未満のインスタンスは、最大 4 つのブロック・ストレージ 2 次ボリュームを接続できます。

4 つ以上の vCPU を持つインスタンスは、最大 12 個のブロック・ストレージ 2 次ボリュームを接続できます。

## IOPS のプロビジョニング時に、割り振られた IOPS はインスタンス単位で適用されるのですか、ボリューム単位で適用されるのですか?
{: faq}

IOPS はボリューム・レベルで適用されます。

## IOPS が測定される方法とは? 
{: faq}

IOPS は、ランダムな 50% の読み取りと 50% の書き込みを使って、16 KB のブロックのロード・プロファイルに基づいて測定されます。このプロファイルと異なるワークロードでは、パフォーマンスが低下する場合があります。

## IOPS プロファイルとは?
{: faq}

IOPS プロファイルは、さまざまな容量のボリュームの IOPS/GB パフォーマンスを定義します。保証された IOPS パフォーマンスを提供する、事前定義された 3 つの [IOPS ティア](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-profiles#tiers)があり、ワークロード要件を満たすようにその中から選択できます。[カスタム IOPS](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-profiles#custom) を定義して、選択したボリューム・サイズの IOPS の範囲を指定することもできます。カスタム IOPS は、事前定義された IOPS ティアの範囲に収まらない、明確に定義されたパフォーマンス要件がある場合に適しています。

## データ・ボリュームで予想される最大 IOPS は何ですか?
{: faq}

データ・ボリュームの最大 IOPS は、ボリューム・サイズと選択した IOPS ティアプロファイルによって異なります。例えば、1 TB までの汎用ボリュームの最大 IOPS は 3,000 IOPS です。詳しくは、[階層化 IOPS プロファイル](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-profiles#tiers)を参照してください。[カスタム IOPS プロファイル](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-profiles#custom) を選択する場合は、指定したボリューム・サイズに対応する最小と最大の範囲も定義します。

## パフォーマンスの測定時に小さなブロック・サイズを使用した場合、どのようになりますか?
{: faq}

小さいブロック・サイズを使用する場合でも最大 IOPS は得られますが、スループットが低くなります。例えば、6000 IOPS のボリュームの場合、さまざまなブロック・サイズでのスループットは以下のようになります。

* 16 KB * 6000 IOPS == ~93.75 MB/秒
* 8 KB * 6000 IOPS == ~46.88 MB/秒
* 4 KB * 6000 IOPS == ~23.44 MB/秒

## 使用量に応じて課金されるのですか? また、割り当て量に制限はありますか?
{: faq}

請求方法について詳しくは、[Block Storage for VPC の料金](/docs/vpc-on-classic?topic=vpc-on-classic-block-storage-pricing)を参照してください。いくつかの制限が適用されます。{{site.data.keyword.cloud}} Virtual Private Cloud およびその内部で使用可能なリソースの割り当て量と制限について詳しくは、[割り当て量](/docs/vpc-on-classic?topic=vpc-on-classic-quotas#quotas)を参照してください。

## ボリュームを作成し、後からその容量を増やすことはできますか?
{: faq}

いいえ。ボリュームの容量を増やすことはできません。ブロック・ストレージ・ボリュームをプロビジョンする前に、予想される増加を十分に考慮した容量を見積もることをお勧めします。

## 期待するスループットを実現するために、ボリュームをプリウォームしておく必要はありますか?
{: faq}

ボリュームをプリウォームする必要はありません。ボリュームをプロビジョンすると、ただちに指定したスループットになります。

## 暗号化ボリュームを作成することはできますか?
{: faq}

すべてのブロック・ストレージ・ボリュームは、IBM 管理の暗号化 (デフォルト) またはお客様の暗号鍵を使用した Key Protect サービスによって暗号化されます。詳しくは、[お客様管理の暗号化を使用したブロック・ストレージ・ボリュームの作成](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-encryption)を参照してください。

## ボリュームの暗号化のタイプは、どのように判別できますか?
{: faq}

UI から、すべてのブロック・ストレージ・ボリュームのリストを表示すると、「暗号化」列にプロバイダー管理の暗号化なのかお客様管理の暗号化なのかが示されます。

CLI からボリュームのプロパティーを表示するには、次のように入力します。

```bash
ibmcloud is volume (VOLUME_NAME | VOLUME_ID)
```

## データはどれほど安全に保管されるのですか?
{: faq}

すべてのブロック・ストレージ・ボリュームは、IBM 管理の暗号化または独自の暗号鍵を使用して、保存中に暗号化されます。IBM 管理鍵は生成後、Consul に支えられているブロック・ストレージ・ボールトに安全に保管され、システムによって保守されます。お客様管理の鍵は、IBM Key Protect サービスを使用して安全に管理されます。

## 災害復旧のためのデータ・バックアップは、どうすればよいですか?
{: faq}

Block Storage for VPC は、地域内の冗長フォールト・ゾーン間のデータを保護します。また、お客様の側でもデータを独自にバックアップすることをお勧めします。ボリューム・クローン作成、スナップショット、複製などの災害復旧機能を提供する [{{site.data.keyword.blockstoragefull}}](/docs/infrastructure/BlockStorage?topic=BlockStorage-getting-started) の使用を検討することもお勧めします。

## ボリュームはいくつプロビジョンできますか?
{: faq}

地域ごとに最大 1,000 のブロック・ストレージ・ボリュームをプロビジョンできます。

## ボリュームの管理に使用すべき戦略は何ですか?
{: faq}

予想される増加に基づいて、必要な容量を決定します。ボリューム・サイズは、プロビジョニング後に拡張することができません。ただし、必要に応じて新しいボリュームを作成できます。また、十分に定義されたパフォーマンス要件がある場合は、ボリューム・サイズごとに特定の IOPS 範囲を提供する[カスタム IOPS](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-profiles#custom) を選択することもできます。

## 仮想サーバー・インスタンスのブート・ディスクはどのように作成され、イメージ・ファイルにどのように関連していますか?
{: faq}

ブート・ディスク (ブート・ボリュームとも呼ばれる) は、仮想サーバー・インスタンスのプロビジョニング時に作成されます。インスタンスのブート・ディスクは、仮想マシン・イメージの複製イメージです。ブート・ボリュームは、接続先のインスタンスを削除すると削除されます。

## ファイアウォールまたはセキュリティー・グループはパフォーマンスに影響しますか?
{: faq}

ベスト・プラクティスとして、ストレージ・トラフィックはファイアウォールをバイパスする VLAN 上を実行することをお勧めします。 ソフトウェア・ファイアウォールを介してストレージ・トラフィックを実行すると、待ち時間が増加し、ストレージ・パフォーマンスに悪影響を与えます。

## ブロック・ストレージ・データ・ボリュームはいつ削除できますか?
{: faq}

ブロック・ストレージ・データ・ボリュームは、仮想サーバー・インスタンスに接続されていない場合にのみ削除できます。削除する前に、[ボリュームを切り離して](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-managing-block-storage#detach)してください。ブート・ボリュームは、インスタンスが削除されると切り離され、削除されます。

## ブロック・ストレージ・データ・ボリュームを削除するとデータはどうなりますか?
{: faq}

ブロック・ストレージ・データ・ボリュームを削除すると、そのボリューム上のデータを指すポインターはすべて除去され、データは完全にアクセス不能になります。後で物理ストレージを別のアカウントに再プロビジョンすると、新しいポインターのセットが割り当てられます。この新しいアカウントが、物理ストレージ上に存在していた可能性のあるデータにアクセスするための方法はありません。新しいポインター・セットはすべて 0 を示します。新しいデータがボリュームに書き込まれると、アクセス不能なデータは上書きされます。

## ブロック・ストレージで予期されるパフォーマンスの待ち時間はどれくらいですか?
{: faq}

ストレージ内の目標待ち時間は 1 ミリ秒未満です。ブロック・ストレージは共有ネットワーク上のコンピュート・インスタンスに接続されるため、正確なパフォーマンス待ち時間は、それぞれの時間フレーム内のネットワーク・トラフィックに依存します。

## マルチゾーン・クラスターで共有ストレージをセットアップできますか?
{: faq}

IBM Cloud では、ストレージ・オプションはアベイラビリティー・ゾーンにローカライズされています。複数のゾーンにまたがって共有ストレージを管理することはお勧めしません。

複数のゾーンおよび地域でデータを共有する必要がある場合は、代わりに {{site.data.keyword.cos_full}} や {{site.data.keyword.cloudantfull}} などの IBM Cloud データ・クラシック・サービス・オプションを使用してください。

## クラシック・インフラストラクチャーにボリュームがあります。それらを VPC に移植できますか?
{: faq}

いいえ。VPCは、マルチゾーン地域内の新しいアベイラビリティー・ゾーンへのアクセスを提供します。コンピュート・リソース、ネットワーク・リソース、およびストレージ・リソースは、VPC で機能するように特別に設計されています。