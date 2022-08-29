---
title: "5GのOSSってどこまで使えるの？"
date: 2022-02-12T23:40:00+09:00
draft: true
slug: 5g_oss
---

## はじめに

5Gあるいは5Gサービスと聞くとモバイルキャリアにより提供されるネットワークサービスで、大手ベンダ製品を使ってモバイルネットワークが構築されているイメージを持たれる方も多いのではないでしょうか。

最近では、5Gネットワークをオープンソースソフトウェア（以下、OSS）で実現する動きが出始めており、個人でも手軽に5G環境を構築することが可能となっています。

本記事では、5GのOSSについて紹介したいと思います。


## そもそも、モバイルネットワークとは?

「端末 (User Equipment)」、「無線アクセスネットワーク (Radio Access Network) 」、「コアネットワーク (Core Network)」の３要素から構成される無線通信設備を指しています。

端末＝スマホ、無線アクセスネットワーク＝基地局、コアネットワーク＝認証サーバやルータ等をイメージするとわかりやすいかと思います。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/490507/6fccda6e-db9a-3fb3-0fcb-3645d1c92d63.png)

## 5GのOSSについて

5GのOSSについて、構成要素（UE/RAN/CN）ごとにそれぞれコミュニティがあり、開発が行われています。

### RAN
代表的な、OpenAirInterfaceCとUERANSIMについて記載します。それ以外にも、srsRANやSD-RANe等のOSSがあります。

- [OAI-RAN](https://gitlab.eurecom.fr/oai/openairinterface5g/)
  - OpenAirInterface Software Alliance(OSA)が提供する3GPPプロトコルに準拠した無線アクセスネットワーク系（eNB/gNB/UE）のソフトウェア
  - 3GPP仕様に則り開発されているため、リファレンスコードとしても利用される
  
- [UERANSIM](https://github.com/aligungr/UERANSIM) 
  - オープンソースの5G端末（UE）や無線アクセスネットワーク（RAN）を実装
  - 主にコアネットワークと接続するための上位レイヤーのプロトコル(NGAP,NASなど)が実装されている

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/490507/b4f8e37d-5b9c-d86f-9d2c-77907c322104.png)

### CN
代表的な、free5GCとOpen5GSについて記載します。それ以外にも、magmaやSD-Core等、様々なOSSがあります。

- [free5GC](https://github.com/free5gc/free5gc)
  - 3GPP Realse15に準拠したオープンソースソフトウェアの5Gコアであり、StandAlone（SA）構成に対応
  - 様々なネットワークファンクションを実装（NRF/AMF/AUSF/SMF/PCF/UDM/UDR/NSSF/UPF/N3IWF）
  - コミュニティの動きも活発で、「[free5GC forum](https://forum.free5gc.org/)」も存在
  
- [Open5GS](https://github.com/open5gs/open5gs) 
  - C言語で実装された、オープンソースソフトウェアの5Gコア及びEPC
  - 3GPP Realse16に準拠し、StandAlone（SA）構成に対応

- [OAI-CN](https://gitlab.eurecom.fr/oai/cn5g) 
  - OpenAirInterface Software Alliance(OSA)が提供する3GPPプロトコルに準拠したコアネットワーク系（EPC and 5G）のソフトウェア
  - 3GPP仕様に則り開発されているため、リファレンスコードとしても利用される

- [magma](https://github.com/magma) 
  - 新興国にコネクティビティを届けることを目的に開発が始まったOSS。EPCの機能(A-GW)だけではなく集中管理機能(Orchestrator)やMNOとの連携機能(F-GW)を有する。
  - 5Gコアについては、Telecom Infra Projectと連携して最小構成版Minimum Viable Core(MVC版)を開発中。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/490507/394eec47-1f6c-461c-3531-74e2b12465a6.png)

## 5GのOSSってどこまで使えるの？
5GのOSSも様々なコミュニティで開発が進んでいる状況で、群雄割拠の状態です。
OSS実装の完成度や、特徴について、[free5GC](https://github.com/free5gc/free5gc)を例に記載します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/490507/29ee0192-3c65-e110-ba51-e202b43ef1ce.png)

* 小規模に実証実験を行うレベルまでは、5GコアのOSSも成長してきており、5G特有の機能・実装も進んでいます。
* 構築も簡単で導入しやすいのですが、商用を見据えると、性能面や運用面でまだまだ課題が残る状況です。

## 5GのOSS関連で困ったことがあったら
モバイルネットワークに関連するOSSの開発者・ユーザ同士で情報交換や新たな繋がりを形成する場として、[Open Mobile Network Infra Community](https://omni-jp.github.io/)を活用してみてはいかがでしょうか。

過去のMeetupやHands-onについてもYouTubeにて公開しております。
イベントの様子がわかると思いますので、ぜひご覧ください。

https://www.youtube.com/channel/UCnZp6DJTQQfoT6rLt8CBz5g

また、情報交換の場としてOpen Mobile Network Infra CommunityのSlackワークスペースも用意しています。

https://join.slack.com/t/omni-jp/shared_invite/zt-nrwl8rw3-gZIS1FckzeQ2efagTrWUpA

これまでの活動成果は以下のgithubにまとめております。ぜひご覧ください。

https://github.com/omni-jp

## 最後に
5GのOSSにより、モバイルネットワークを自営でかつ簡単に構築可能になりつつあります。
この機会にお手元のPCで5G環境を構築してみてはいかがでしょうか？
