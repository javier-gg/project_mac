## Python 3.13 en Debian 11 (ARM64) para Apple Silicon
FROM --platform=linux/arm64 python:3.13-bullseye

ENV DEBIAN_FRONTEND=noninteractive

## Sistema base, utilidades y dependencias mínimas para R
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    git \
    vim \
    pandoc \
    pandoc-citeproc \
    gdebi-core \
    r-base \
    r-base-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    libfontconfig1 \
    fonts-dejavu \
    && rm -rf /var/lib/apt/lists/*

## Instalar Quarto CLI ARM64 (ajusta versión si sale una nueva)
#RUN curl -LO https://github.com/quarto-dev/quarto-cli/#releases/download/v1.5.47/quarto-1.5.47-linux-arm64.deb \
#    && gdebi --non-interactive quarto-1.5.47-linux-arm64.deb \
#    && rm -f quarto-1.5.47-linux-arm64.deb

RUN curl -LO https://quarto.org/download/latest/quarto-linux-arm64.deb \
    && gdebi --non-interactive quarto-linux-arm64.deb \
    && rm -f quarto-linux-arm64.deb


## Instalar aquí los paquetes base de R
#RUN R -e "install.packages(c('tidyverse', 'languageserver'), repos='https://cloud.r-project.org')"

# Instala requerimientos de Python
COPY requirements.txt /app/requirements.txt
WORKDIR /app
RUN pip install --upgrade pip
RUN pip install -r /app/requirements.txt

WORKDIR /workspace

EXPOSE 8888

CMD ["bash"]
