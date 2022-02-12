---
title: "UEのIPアドレスの割り当て -- free5GC編 --"
date: 2021-11-25T15:40:00+09:00
draft: true
---

## はじめに

5GではUEのIPアドレスは、どのような仕組みで割り当てられるのでしょうか?
5GCがDHCPサーバーの機能を保有しているのでしょうか?
はたまた、5GCとは別にRADIUSサーバーが存在しており、5GCとRADIUSサーバーが連携することでIPアドレスが割り当てられるのでしょうか?

UEのIPアドレスの割り当てについて、free5GCではどのように実現しているのか解説したいと思います。


## 5Gの規格ではどうなっているのか?

TS 23.501の5.8.2.2 UE IP Address Managementで詳細な仕様が述べられていますが、ざっくりまとめると以下の仕様になっています。

* NGAP/NASを通してUEとSMFの間でPDU Session Typeがやりとりされる。
* PDU Session TypeによってIPv4かIPv6か決まる。
* IPアドレスの割り当ては大きくわけて2種類ある。
  1. PDU Session確立後にDHCPもしくはDN-AAAを利用してIPアドレスの割り当てを行う。
  2. PDU Sessionの確立中にSMFがSM NAS Signalingを介してUEのIPアドレスを送信する。

DHCPやDN-AAA以外にもSMFが割り当てるという仕様も存在することがわかりました。
では実際にfree5GCではどのような実装になっているのか追ってみたいと思います。


## パケットキャプチャで確認

UERANSIMとfree5GCで簡単な構成を組んでパケットをキャプチャして確認してみます。

DHCPやDN-AAAであれば、N3のU-Plane側でそれぞれのプロトコルのやりとりがあるはずです。 一方で、SMFが割り当てる方式であればSM NAS Signalingの中にUEのIPアドレスが入っていることが確認できるはずです。

N3のU-Plane側のキャプチャを見てみましょう。

![Pic](n3.png)

UEのIPアドレスが確定した状態のパケットしかありません。
