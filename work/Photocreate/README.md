# 株式会社フォトクリエイト

## 期間

2022年11月～2023年3月

## 業務形態

業務委託

## 担当業務

今回の開発は大きく分けて以下の2つに分かれていました：  
1. Windowsデスクトップアプリの開発  
2. スマホアプリの開発  

私は主にWindowsのデスクトップアプリ開発と、Lambdaを用いたバックエンド開発を担当しました。

---

## 業務内容

### デスクトップアプリ開発

- **使用技術**  
  - Electron  
  - Electron-updater  
  - Next.js  
  - TypeScript  
  - TailwindCSS  
  - GitHub Actions  

- **開発概要**  
  メインプロセスをTypeScriptで、レンダラープロセスをNext.jsで開発しました。  
  使用したフレームワーク:  
  [https://github.com/vercel/next.js/tree/canary/examples/with-electron-typescript](https://github.com/vercel/next.js/tree/canary/examples/with-electron-typescript)  

  主な処理は、メインプロセスで画像データを取得し、AWS SDKを使用してS3にアップロードするというものでした。  
  デプロイにはElectron-updaterを使用し、GitHubのReleaseにアップロード。さらにGitHub Actionsを活用して、自動デプロイの仕組みを構築しました。

---

### Lambdaを用いたバックエンド開発

- **使用技術**  
  - AWS CDK  
  - AWS SDK  
  - Webpack  
  - Squoosh  
  - Jest  

- **開発概要**  
  S3に画像がアップロードされた際に以下の処理を自動化するLambdaを構築しました：  
  1. **画像のグルーピング処理**  
     - 画像のメタデータ（撮影時間）を参照し、撮影時間が近いものをグルーピング。  
     - グルーピング結果をJSON形式でS3に保存。  
  2. **画像圧縮処理**  
     - 圧縮用の画像を生成し、S3に保存。  

  **課題と解決策**  
  - 画像圧縮処理ではSquooshライブラリを使用しましたが、Lambda環境においてSquooshのWASMファイルを含めてデプロイする必要がある点で苦労しました。  
  - Webpackを使用してSquooshの必要なモジュールを含めたデプロイパッケージを作成することで解決しました。

---

## プロジェクト概要

保育園の先生がCanonの自動撮影カメラ「Pick」で撮影した児童の写真を、以下のフローで保護者が確認できるサービスです：

1. **撮影**: 先生がPickで児童を撮影。  
2. **画像アップロード**: PickとPCをUSBで接続すると、画像データが自動でアップロードされる。  
3. **保護者確認**: 保護者がスマホアプリで画像を確認可能。  
