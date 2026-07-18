FROM ubuntu:24.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    qemu-system-x86 \
    novnc \
    websockify \
    curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /liveos

# ? PASTE YOUR DIRECT ISO DOWNLOAD LINK BETWEEN THE QUOTES BELOW
RUN curl -L -o /liveos/my-custom-os.iso "https://github.com/nugasnugis/AxelOS/releases/download/v0.1-phase1/axelos-amd64.iso"

RUN echo '#!/bin/sh\n\
qemu-system-x86_64 -m 3500 -smp 2 -cdrom /liveos/my-custom-os.iso -snapshot -vnc :0 -vga std &\n\
websockify --web /usr/share/novnc 6080 localhost:5900\n\
' > /usr/local/bin/start-os.sh && chmod +x /usr/local/bin/start-os.sh

EXPOSE 6080
CMD ["/usr/local/bin/start-os.sh"]
