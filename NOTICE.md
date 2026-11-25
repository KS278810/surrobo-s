# NOTICE

SurRobo-S は、次のソフトウェアに依存する。表のうち、同梱と書いたものだけがこのリポジトリに入る。ほかは導入時に入れるか、実行時に読む。

## 探索エンジン
- symbolic_regression 0.12.3 と dynamic_expressions 0.10.1、Apache-2.0。SymbolicRegression.jl の Rust 版で、`engine_rs/` の探索コマンドが使う。ライセンスの文は `licenses/symbolic_regression.rs-Apache-2.0.txt`。Rust の依存 29 件はすべて MIT か Apache-2.0 か両方で、一覧は `engine_rs/LICENSES.txt`。版は `engine_rs/Cargo.lock` で固定する。2 つの crate の写しを `engine_rs/vendor/` に置き、違いは 2 か所だけで、`engine_rs/vendor/README.md` に書いた。写しにも同じ Apache-2.0 の LICENSE を添えた。
- ブラウザ版の探索は `surrobo_s/engine_pipeline.py` で、2 段になる。第 1 段は `surrobo_s/engine_light.py` で、numpy と sympy だけを使う。第 2 段は symbolic_regression_wasm 0.7.5、Apache-2.0、の WebAssembly 版で、`engine_rs/wasm/` で作り、ページが共有メモリを使えるときだけ読む。その Rust の依存 52 件は、すべて MIT、Apache-2.0、Unlicense、BSL-1.0 のいずれかで、一覧は `engine_rs/LICENSES.txt`。wasm-bindgen-rayon 1.3.0 は Apache-2.0、Copyright 2022 Google Inc.。ライセンスの文は `licenses/symbolic_regression.rs-Apache-2.0.txt` と同じ Apache-2.0 の本文で、補助ファイルの先頭にも付く。

## 画面と実行環境
- numpy、sympy、FastAPI、uvicorn。画面とコード生成に使う。
- scikit-learn、BSD-3-Clause。列の上限のときだけ使う。
- Pyodide 0.28.0、MPL-2.0。ブラウザ版のページが `vendor/pyodide/` に同梱して自分で配る。取得は `_shared/publish/fetch_vendor.py` で、公式の配布物を sha256 で確かめる。変更せずに配るので、この製品にソースの開示の義務は生じない。MPL の対象ファイルのソースは https://github.com/pyodide/pyodide の 0.28.0 にあり、ライセンスの文は `licenses/Pyodide-MPL-2.0.txt`。同梱の wheel は numpy、scipy、scikit-learn、sympy、mpmath、joblib、threadpoolctl、OpenBLAS で、どれも変更せず、それぞれのライセンスの文は wheel の中の dist-info にある。Python の標準ライブラリ `python_stdlib.zip` は CPython 3.13.2 で、PSF License Agreement、文は `licenses/CPython-PSF-3.13.txt`。OpenBLAS 0.3.26 は BSD-3-Clause で、文は `licenses/OpenBLAS-BSD-3-Clause.txt`。`python3 ../_shared/licenses/vendor_notice.py check ../_public/surrobo-s/vendor/pyodide NOTICE.md` は、同梱の部品がこの文書に無いと失敗する。
- coi-serviceworker 0.1.7、MIT、Copyright 2021 Guido Zuidhof。同梱。ページを cross-origin isolated にして、第 2 段の WebAssembly が共有メモリを使えるようにする。GitHub Pages は応答ヘッダーを設定できないため、service worker が代わりに付ける。ライセンスの文は `licenses/coi-serviceworker-MIT.txt`。
- numpy と scipy の Linux 向けのビルド済みの配布物が、libgfortran、GPL-3.0-or-later と GCC ランタイム例外、libquadmath、LGPL-2.1-or-later、OpenBLAS、BSD-3-Clause を内蔵することは、2026-11-01 の調査で記録したが、再確認していない。ページが配るのは wasm 用の wheel で、2026-11-10 にそのファイル一覧を調べたところ、libgfortran、libquadmath、`.libs` のファイルは 1 つも無かった。一覧だけでは、コンパイル済みの本体への静的な組み込みは分からないので、wasm の wheel についてこの項目は未確認のまま残す。Linux 向けの wheel を含む venv ごと顧客に渡すときは、libgfortran と libquadmath の条件を満たす。ソースは GCC のプロジェクトにあり、https://gcc.gnu.org/ で入手できる。変更は加えていない。
- KaTeX 0.16.11、MIT。同梱。`surrobo_s/web/static/katex` にあり、フォントも同じ MIT で、ライセンスの文は同じフォルダの LICENSE。出典は katex-fonts の LICENSE、2018 Khan Academy。
- Chakra Petch、SIL OFL 1.1、Copyright 2018 The Chakra Petch Project Authors。画面の見出しの字体で、woff2 を `index.html` に埋め込んでいる。ライセンスの文は `licenses/ChakraPetch-OFL-1.1.txt`。
- IBM Plex Mono、SIL OFL 1.1、Copyright 2017 IBM Corp. with Reserved Font Name Plex。画面の等幅の字体で、woff2 を `index.html` に埋め込んでいる。ライセンスの文は `licenses/IBMPlexMono-OFL-1.1.txt`。字体の名前 Plex は予約されているので、字体を改変したときは別の名前にする。

## 公開用の複製を作る道具
- terser、BSD-2-Clause。javascript-obfuscator、BSD-2-Clause。python-minifier、MIT。公開用の複製を作る `_shared/robo publish` だけが使い、成果物には含めない。

## 製品としての条件
- このリポジトリの本体は CC BY-NC 4.0 で、商用利用を許さない。商用にするときは LICENSE と、README と、画面の文を新しいライセンスに直す。公開済みの複製は CC BY-NC のまま残る。
- 画面のマスコットは、静止画が Qwen-Image、動きが Wan 2.2 で作られ、どちらも Apache-2.0。H3 の制限は受けない。
