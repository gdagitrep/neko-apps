ARG BASE_IMAGE=ghcr.io/m1k1o/neko/base:latest
FROM $BASE_IMAGE

# Install any necessary dependencies
RUN set -eux; apt-get update; \
    apt-get install -y --no-install-recommends \
    libglib2.0-0 \
    libx11-6 \
    libxcb1 \
    libxcomposite1 \
    libxcursor1 \
    libxdamage1 \
    libxext6 \
    libxi6 \
    libxrandr2 \
    libxrender1 \
    libxss1 \
    libxtst6 \
    libnss3 \
    libasound2 \
    python3-pip; \
    apt-get clean -y; \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/* /tmp/*;

# Install Python dependencies
RUN pip3 install six

# Copy the new binary (built with GLIBC 2.31)
COPY Dafri /usr/local/bin/dafri
RUN chmod +x /usr/local/bin/dafri

# Create supervisord configuration
RUN mkdir -p /etc/neko/supervisord && \
    echo '[program:dafri]\n\
command=/usr/local/bin/dafri\n\
autorestart=true\n\
priority=100\n\
stdout_logfile=/dev/stdout\n\
stdout_logfile_maxbytes=0\n\
stderr_logfile=/dev/stderr\n\
stderr_logfile_maxbytes=0\n' > /etc/neko/supervisord/dafri.conf 