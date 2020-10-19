# mbedtls-static-libgcc-package


## 概要
- mbedTLS ( https://github.com/ARMmbed/mbedtls ) の  
  MSYS2/MinGW-w64 環境用のパッケージファイルを  
  配布するリポジトリです。

- 標準の mbedTLS パッケージとの違いは、libgcc を static link にしたことです。  
  このため、成果物を配布する場合に、  
  libgcc_s_seh-1.dll (64bit 環境の場合) や libgcc_s_dw2-1.dll (32bit 環境の場合) を、  
  配布する必要がありません。  
  ( libmbedtls.dll , libmbedcrypto.dll , libmbedx509.dll のみを配布すればよい)

- PKGBUILD ファイルは、以下のものをベースに変更しました。  
  https://github.com/msys2/MINGW-packages/blob/e1cb17b01e55e79a536d2f6523dfbbfd4698668b/mingw-w64-mbedtls/PKGBUILD


## インストール方法
- MSYS2/MinGW-w64 (64bit/32bit) 環境での、本パッケージのインストール手順を、  
  以下に示します。

1. MSYS2/MinGW-w64 (64bit/32bit) のインストール  
   事前に MSYS2/MinGW-w64 (64bit/32bit) がインストールされている必要があります。  
   以下のページを参考に、開発環境のインストールを実施ください。  
   https://gist.github.com/Hamayama/eb4b4824ada3ac71beee0c9bb5fa546d  
   (すでにインストール済みであれば本手順は不要です)

2. パッケージファイルのダウンロード  
   以下のリリースページから、環境に応じたパッケージファイルをダウンロードして、  
   適当な作業用フォルダに置いてください。  
   (作業用フォルダのパスには、空白を入れないようにしてください)  
   
   https://github.com/Hamayama/mbedtls-static-libgcc-package/releases  
   
   ( i686 は 32bit 環境用で、x86_64 は 64bit 環境用になります)

3. パッケージファイルのインストール  
   ダウンロードしたパッケージファイルを、開発環境にインストールします。  
   
   ＜MSYS2/MinGW-w64 (64bit) 環境の場合＞  
   プログラムメニューから MSYS2 の MinGW 64bit Shell を起動して、以下のコマンドを実行してください。  
   ( c:\work にパッケージファイルを置いた場合)
   ```
     cd /c/work
     pacman -U mingw-w64-x86_64-mbedtls-static-libgcc-2.16.5-2-any.pkg.tar.xz
   ```
   ＜MSYS2/MinGW-w64 (32bit) 環境の場合＞  
   プログラムメニューから MSYS2 の MinGW 32bit Shell を起動して、以下のコマンドを実行してください。  
   ( c:\work にパッケージファイルを置いた場合)
   ```
     cd /c/work
     pacman -U mingw-w64-i686-mbedtls-static-libgcc-2.16.5-2-any.pkg.tar.xz
   ```

- 以上です。


## 保守用メモ
1. プログラムメニューから MSYS2 の MinGW 64bit Shell を起動して、  
   以下のコマンドを実行すると、パッケージファイルが生成される。  
   (事前に CMake のインストールが必要)
   ```
     cd /c/work/mbedtls-static-libgcc-package
     makepkg-mingw
   ```
   その後、GitHub の Releases ページでリリースを作成して、  
   パッケージファイルをアップロードする。


## 環境等
- OS
  - Windows 10 (version 1909) (64bit)
- 環境
  - MSYS2/MinGW-w64 (64bit) (gcc version 10.2.0 (Rev1, Built by MSYS2 project))

## 履歴
- 2020-10-14 mbedtls-static-libgcc 2.16.5-1 のパッケージファイルを作成
- 2020-10-15 mbedtls-static-libgcc 2.16.5-2 のパッケージファイルを作成  
  (フォルダ指定ミス修正)


(2020-10-19)
