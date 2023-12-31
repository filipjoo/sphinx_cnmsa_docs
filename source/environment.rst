========================================
windowsにsphinxをインストール方法のメモ
========================================

1. chocolateyをインストール
-------------------------------
※最初からインストールされてたのでver確認だけ。

.. code-block::

    PS C:\Users\niiis> choco
    Chocolatey v1.2.1
    Please run 'choco -?' or 'choco <command> -?' for help menu.

2. pythonをインストール
------------------------
※最初からインストールされてたのでver確認だけ。

.. code-block::

    PS C:\Users\niiis> python --version
    Python 3.10.10

3. sphinxをインストール
------------------------

.. code-block::

    pip install -U sphinx
    ・・・
    Successfully installed Pygments-2.16.1 alabaster-0.7.13 babel-2.13.0 docutils-0.20.1 imagesize-1.4.1 packaging-23.2 snowballstemmer-2.2.0 sphinx-7.2.6 sphinxcontrib-applehelp-1.0.7 sphinxcontrib-devhelp-1.0.5 sphinxcontrib-htmlhelp-2.0.4 sphinxcontrib-jsmath-1.0.1 sphinxcontrib-qthelp-1.0.6 sphinxcontrib-serializinghtml-1.1.9

    [notice] A new release of pip available: 22.3.1 -> 23.3.1
    [notice] To update, run: python.exe -m pip install --upgrade pip

pythonのversion確認がうまくいかないときの参考リンク
https://gammasoft.jp/blog/python-change-environment-variables-after-installed/

4. sphinxのversion確認
------------------------
.. code-block::

    PS C:\Users\niiis> sphinx-build --version
    sphinx-build 7.2.6

versionが見れるのでOK

5. sphinx-quickstartでプロジェクト(cnmsa_level1)作成
------------------------------------------------------------------------

.. code-block::

    PS C:\workspace> sphinx-quickstart
    Welcome to the Sphinx 7.2.6 quickstart utility.

    Please enter values for the following settings (just press Enter to
    accept a default value, if one is given in brackets).

    Selected root path: .

    You have two options for placing the build directory for Sphinx output.
    Either, you use a directory "_build" within the root path, or you separate
    "source" and "build" directories within the root path.
    > Separate source and build directories (y/n) [n]: y

    The project name will occur in several places in the built documentation.
    > Project name: cnmsa_level1
    > Author name(s): Seiya
    > Project release []: release-0.1

    If the documents are to be written in a language other than English,
    you can select a language here by its language code. Sphinx will then
    translate text that it generates into that language.

    For a list of supported codes, see
    https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-language.
    > Project language [en]: ja

    Creating file C:\workspace\source\conf.py.
    Creating file C:\workspace\source\index.rst.
    Creating file C:\workspace\Makefile.
    Creating file C:\workspace\make.bat.

    Finished: An initial directory structure has been created.

    You should now populate your master file C:\workspace\source\index.rst and create other documentation
    source files. Use the Makefile to build the docs, like so:
    make builder
    where "builder" is one of the supported builders, e.g. html, latex or linkcheck.

6. sphinx_rtd_themeをインストール
------------------------------------------------

.. code-block::

    $ pip install sphinx_rtd_theme
    ・・・
    Successfully installed docutils-0.18.1 sphinx_rtd_theme-1.3.0 sphinxcontrib-jquery-4.1


7. sphinx_rtd_themeの確認
------------------------------------------------
.. code-block::

    pip list / freeze
    Package                       Version
    ----------------------------- ---------
    ・・・
    sphinx-rtd-theme              1.3.0

入ってるのでOK

8. cnmsa_level1にsphinx_rtd_themeを設定
------------------------------------------------
conf.pyの編集

# sphinx_rtd_themeの設定
.. code-block::

    html_theme = 'sphinx_rtd_theme'

9. ビルド
------------------------
.. code-block::

    PS C:\workspace\sphinx_cnmsa> .\make html
    Running Sphinx v7.2.6
    ・・・
    build succeeded.

    The HTML pages are in build\html.

10. github pagesにあげるための設定
------------------------------------------------
https://github.com/filipjoo/sphinx_cnmsa_docs/settings/pages
でBranchをmain/docsに変更してURL取得

11. リビルド
------------------------
make.batを編集

.. code-block::

    - set BUILDDIR=build
    + set BUILDDIR=./docs
    - %SPHINXBUILD% -M %1 %SOURCEDIR% %BUILDDIR% %SPHINXOPTS% %O%
    + %SPHINXBUILD% -b %1 %SOURCEDIR% %BUILDDIR% %SPHINXOPTS% %O%

    PS C:\workspace\sphinx_cnmsa> .\make html

12. リビルドしたファイルをgithubにpush
------------------------------------------------
省略


XX. 参考
------------------------

https://zenn.dev/y_mrok/books/sphinx-no-tsukaikata/viewer/chapter8