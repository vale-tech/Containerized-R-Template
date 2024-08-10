FROM rocker/tidyverse:latest

LABEL org.opencontainers.image.licenses="GPL-2.0-or-later" \
      org.opencontainers.image.source="https://github.com/rocker-org/rocker-versioned2" \
      org.opencontainers.image.vendor="Rocker Project" \
      org.opencontainers.image.authors="Carl Boettiger <cboettig@ropensci.org>"

# Proxy Configuration See README
# COPY certs/. /usr/local/share/ca-certificates/
# ENV NODE_EXTRA_CA_CERTS=/usr/local/share/ca-certificates/WC-Decrypt-Cert.crt
# RUN update-ca-certificates

# My R packages
RUN install2.r languageserver vscDebugger \
              here rmarkdown pagedown \
              readxl tictoc ggthemes ggrepel lubridate gt knitr scales zoo \
    && rm -rf /tmp/downloaded_packages