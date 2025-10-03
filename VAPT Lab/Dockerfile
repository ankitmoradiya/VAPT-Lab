FROM kalilinux/kali-rolling

LABEL maintainer="Ankit Moradiya"

# Environment
ENV HOME /root
ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /root

# Update & Install essentials
RUN apt-get update && apt-get install -y --no-install-recommends \
    git wget curl unzip python3 python3-pip build-essential \
    nmap jq dnsutils iputils-ping \
    && rm -rf /var/lib/apt/lists/*

# Setup folders
RUN mkdir -p ${HOME}/toolkit ${HOME}/datasharing

# Install Go
RUN cd /opt && \
    wget https://go.dev/dl/go1.22.3.linux-amd64.tar.gz && \
    tar -xvf go1.22.3.linux-amd64.tar.gz && \
    rm -rf go1.22.3.linux-amd64.tar.gz && \
    mv go /usr/local
ENV GOROOT /usr/local/go
ENV GOPATH /root/go
ENV PATH ${GOPATH}/bin:${GOROOT}/bin:${PATH}

# Install Go-based security tools
RUN go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
RUN go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
RUN go install -v github.com/projectdiscovery/nuclei/v2/cmd/nuclei@latest
RUN go install -v github.com/ffuf/ffuf@latest
RUN go install -v github.com/tomnomnom/assetfinder@latest
RUN go install -v github.com/tomnomnom/waybackurls@latest
RUN go install -v github.com/tomnomnom/gf@latest
RUN go install -v github.com/tomnomnom/unfurl@latest
RUN go install -v github.com/hakluke/hakrawler@latest
RUN go install -v github.com/lc/gau/v2/cmd/gau@latest

WORKDIR /root
