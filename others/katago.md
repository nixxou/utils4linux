```sh
#!/bin/sh
cd $(dirname $0)

if [ ! -e dist ]; then
echo ">>> init"
export ALL_PROXY=
export all_proxy=
python3 -m venv dist
cd dist
source bin/activate
pip install katrain # 1.14.0
# pip install -i https://pypi.tuna.tsinghua.edu.cn/simple katrain
spdir=$(python3 -c "import site;print(site.getsitepackages()[0])")
curl -o katago.zip -L https://github.com/lightvector/KataGo/releases/download/v1.13.0/katago-v1.13.0-eigenavx2-linux-x64.zip
unzip -p katago.zip katago >$spdir/katrain/KataGo/katago
rm -f katago.zip
strip -s $spdir/katrain/KataGo/katago
chmod +x $spdir/katrain/KataGo/katago
rm -rf $spdir/ffpyplayer.libs $spdir/pip
strip $(find $spdir -name "*.so")
exit
fi

if [ "$1" = "" ]; then
cd dist
source bin/activate
katrain
exit
fi

# https://github.com/lightvector/KataGo
# https://github.com/leela-zero/leela-zero
# https://github.com/kaorahi/lizgoban

```