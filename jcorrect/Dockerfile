FROM alpine
MAINTAINER R.Kunimoto <ht14a022@oecu.jp>
RUN echo "Install Package"
RUN apk update && \
    apk add ca-certificates && \
    update-ca-certificates && \
    apk add curl && \
    apk add g++ && \
    apk add make && \
    apk add perl

RUN echo "Install CRF++"
RUN cd /tmp && \
    curl -s -L -o CRF++.tar.gz "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7QVR6VXJ5dWExSTQ" && \
    tar xf CRF++.tar.gz && \
    cd CRF* && \
    ./configure && \
    make && make install && \
    cd .. && \
    rm -rf CRF*

RUN echo "Install MeCab"
RUN cd /tmp && \
    curl -s -L -o mecab.tar.gz "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7cENtOXlicTFaRUE" && \
    tar xf mecab.tar.gz && \
    cd mecab* && \
    ./configure && \
    make && make install && \
    cd .. && \
    rm -rf mecab*

RUN echo "Install MeCab IPA-Dic"
RUN cd /tmp && \
    curl -s -L -o mecab-ipa.tar.gz "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7MWVlSDBCSXZMTXM" && \
    tar xf mecab-ipa.tar.gz && \
    cd mecab-ipadic* && \
    ./configure --enable-utf8-only --with-charset=utf8 && \
    make && make install && \
    cd .. && \
    rm -rf mecab*

RUN echo "Install CaboCha"
RUN cd /tmp && \
    curl -c /tmp/cookie.txt -s -L "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7SDd1Q1dUQkZQaUU" |grep confirm |  sed -e "s/^.*confirm=\(.*\)&amp;id=.*$/\1/" | xargs -I{} \
    curl -b /tmp/cookie.txt -s -L -o cabocha.tar.bz2 "https://drive.google.com/uc?confirm={}&export=download&id=0B4y35FiV1wh7SDd1Q1dUQkZQaUU" && \
    tar xf cabocha.tar.bz2 && \
    cd cabocha* && \
    ./configure --with-charset=utf8 --enable-utf8-only && \
    make && make install && \
    cd .. && \
    rm -rf cabocha*

RUN echo "Install jcorrect"
RUN cd /tmp && \
    curl -s -L -o jcorrect.euc http://www.lsnl.jp/~ohsaki/software/perl/jcorrect && \
    iconv -f EUCJP -t UTF8 /tmp/jcorrect.euc > /usr/bin/jcorrect && \
    rm jcorrect.euc && \
    chmod +x /usr/bin/jcorrect

CMD jcorrect