FROM python:3.7-slim-buster

WORKDIR /olympe

# Postinst and env are customized to not use a virtualenv
ENV ENV_DIR=/olympe/products/olympe/linux/env
ENV COMMON_DIR=/olympe/products/olympe/linux
ENV ARSDK_DIR=/olympe/products/olympe
ENV PRODUCT_DIR=/olympe/products
ENV ROOT_DIR=/olympe
ENV MODULES_DIR="${ROOT_DIR}/packages"
ENV MODULES=olympe
ENV PYTHONPATH="$MODULES_DIR/olympe/src"
ENV PYTHONPATH="${PYTHONPATH}:$ROOT_DIR/out/olympe-linux/final/usr/lib/python"
ENV PYTHONPATH="${PYTHONPATH}:${ROOT_DIR}/out/olympe-linux/final/usr/lib/python/site-packages"
ENV PYTHONPATH="${PYTHONPATH}:${ROOT_DIR}/out/olympe-linux/final/usr/local/lib/python"
ENV PYTHONPATH="${PYTHONPATH}:${ROOT_DIR}/out/olympe-linux/final/usr/local/lib/python/site-packages"
ENV PYTHONPATH="${PYTHONPATH}:${ROOT_DIR}/out/olympe-linux/staging-host/usr/lib/arsdkgen"
ENV OLYMPE_LIB_PATH="${ROOT_DIR}/out/olympe-linux/final/usr/lib"
ENV OLYMPE_XML="${ROOT_DIR}/out/olympe-linux/staging-host/usr/lib/arsdkgen/xml"
ENV OLYMPE_GENERATE="${ROOT_DIR}/packages/olympe/src/olympe/"
ENV CLANG_VERSION=6.0
ENV PY_REQS_TXT="${MODULES_DIR}/olympe/requirements.txt"
ENV PATH=/olympe/out/olympe-linux/final/usr/bin:/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/olympe/.local/bin
ENV LD_LIBRARY_PATH=/olympe/out/olympe-linux/final/lib:/olympe/out/olympe-linux/final/usr/lib

RUN apt-get update \
  && apt-get install -y less git curl vim \
    wget libclang-${CLANG_VERSION}-dev \
    build-essential yasm cmake libtool libc6 libc6-dev unzip freeglut3-dev libglfw3 libglfw3-dev libsdl2-dev libjson-c-dev \
    libcurl4-gnutls-dev libavahi-client-dev libgles2-mesa-dev rsync cmake libbluetooth-dev libavahi-client-dev \
    libopencv-dev libswscale-dev libavformat-dev libavcodec-dev libavutil-dev cython \
  && useradd -ms /bin/bash -G root olympe \
  && curl https://storage.googleapis.com/git-repo-downloads/repo > /bin/repo \
  && chmod a+x /bin/repo \
  && git config --global user.name "parrot" \
  && git config --global user.email "parrot@sdk.es" \
  && git config --global color.ui false \
  && repo init -u https://github.com/Parrot-Developers/groundsdk-manifest.git \
  && repo sync \
  && rm /olympe/.repo/manifests/EULA.md \
  && chown -R olympe /olympe


# Run pip as non root user
USER olympe
RUN pip install --no-cache-dir clang~=${CLANG_VERSION} \
  && pip install --no-cache-dir -r $PY_REQS_TXT \
  && ./build.sh -p olympe-linux -A all final -j 

WORKDIR /app
