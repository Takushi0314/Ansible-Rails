# Ansible-Rails
## 概要
---
Ansibleを利用して、CentOS上にApache + Rails + Postgres環境を自動で構築します。  
テンプレート化してあり、ローカル、検証、本番の3つの環境を立ち上げられるようにしてあります。  
(検証と本番のIP等は設定する必要があります。)
また、rubyやrails、postgresqlのバージョンも変更できるので、アプリに応じて変更してください。

## 使い方
---
inventory/(環境)/hostsファイル内のIPアドレスを、構築したいIPアドレスに変更してください。
環境は3種類用意あり、
*	ローカル環境 : local
*	検証環境 : verification
*	本番環境 : production
上記を切り替えて実行します。  
実行元のクライアントにAnsibleをインストールしてある必要があり、構築先(サーバ側)にAnsibleのインストールは必要ありません。  

構築先のOSですが、インストールだけお願いします。  
インストール時似ですが、管理者ユーザだけ作成してください。  
作成したユーザを、hostsファイルで指定してください。  
(AnsibleはSSHで接続して処理を行うので、SSHが解放されていることと、SSHユーザが必要です。普通にインストールすれば自動的に設定された状態になるはずです)  
実行コマンド(localの部分を環境に合わせて変更してください)    
ansible-playbook -i inventories/local/hosts site.yml

## 処理内容
---
*   共通処理 : SELinux無効化, yumのアップグレード, Gitインストール  
*   WEB + AP : Apacheインストール, rbenv, rbuy-build, rubyのインストール, 80番ポート解放  
*   DB : Postgresqlインストール  

## 前提環境
---
*   CentOS 7, 8(動作テストはminimalで行いました)  
*   管理者ユーザは、インストール時に作成してくだい。  

## ミドルウェア環境
---
*   WEB + APサーバ : Apache + Rails(passenger)  
*   DBサーバ : Postgresql  
サンプルでは、1つのサーバ上に上記Apache, Rails, Postgresqlをインストールするようになっています。  
WEBとAPを分ける場合は、必要に応じてインストール先を分けてください。  

## デプロイ
---
デプロイも自動化できまが、本リポジトリをもとに作成してください。  
本リポジトリは、あくまで汎用的に使えるようにしたものです。  
