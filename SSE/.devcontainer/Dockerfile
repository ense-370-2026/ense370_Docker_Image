# Base: Ubuntu with common tools
FROM ubuntu:22.04

# Avoid timezone prompts
ENV DEBIAN_FRONTEND=noninteractive

# Install core packages + Chrome dependencies
RUN apt-get update && apt-get install -y \
    curl git unzip xz-utils zip libglu1-mesa \
    build-essential cmake clang make \
    apt-transport-https software-properties-common \
    libgtk-3-0 libx11-xcb1 libxcomposite1 libxdamage1 libxext6 \
    libxi6 libxtst6 libnss3 libxrandr2 libasound2 libpangocairo-1.0-0 \
    fonts-liberation libappindicator3-1 libgbm1 wget \
    && rm -rf /var/lib/apt/lists/*

# Install Java + Maven for JUnit support
RUN apt-get update && apt-get install -y \
    openjdk-17-jdk \
    maven \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# --- Install Node.js LTS (via Nodesource) ---
RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*

# --- Install Flutter ---
RUN git clone https://github.com/flutter/flutter.git /usr/local/flutter -b stable
ENV PATH="/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin:${PATH}"

RUN flutter --version
RUN flutter precache --web
RUN flutter config --enable-web

# Set default Flutter web port & hostname
ENV FLUTTER_WEB_PORT=8080
ENV FLUTTER_WEB_HOSTNAME=0.0.0.0

# Expose typical Flutter Web port
EXPOSE 8080


# Default to bash
CMD ["/bin/bash"]
