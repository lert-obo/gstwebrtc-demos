FROM maxmcd/gstreamer:1.14-buster

# RUN apt-get install -y libjson-glib-dev
RUN apt update -y --allow-releaseinfo-change
RUN apt-get install -y libjson-glib-dev
# RUN apt install -y json-glib-dev libsoup-dev

WORKDIR /gst-plugins-base-1.14.0
RUN apt install -y libx11-dev
RUN ./configure --prefix=/usr --disable-gtk-doc --enable-x \
    && make \
    && make install

RUN apt-get update && apt-get install -y python3-pip \
                                         pkg-config \ 
                                         libcairo2-dev \
                                         gcc \
                                         python3-dev \
                                         libgirepository1.0-dev \
                                         python-gst-1.0 \
                                         gir1.2-gst-plugins-bad-1.0 

RUN apt install -y gstreamer1.0-plugins-bad \
                                         gstreamer1.0-plugins-good \
                                         gstreamer1.0-nice

RUN apt install -y gstreamer1.0-libav
# RUN apt install -y python3-pip python-gi-dev  
# RUN python3 -m pip install --user websockets

WORKDIR /opt/
COPY . /opt/

RUN pip3 install --no-cache-dir -r requirements.txt

# CMD echo "Waiting a few seconds for you to open the browser at localhost:8080" \
#     && sleep 10 \
#     && ./webrtc-recvonly \
#     --peer-id=1 \
#     --server=ws://signalling:8443 \
#     --disable-ssl


# echo "Waiting a few seconds for you to open the browser at localhost:8080" \
#     && sleep 10 \
#     && ./webrtc-recvonly \
#     --peer-id=1 \
#     --server=ws://192.168.1.61:8443 \
#     --disable-ssl

#  gst-launch-1.0 videotestsrc is-live=true pattern=ball ! videoconvert ! queue ! ximagesink
# gst-launch-1.0 rtspsrc location=rtsp://admin:Obodroid@192.168.1.23/media/video1 ! rtph264depay ! h264parse ! videoconvert ! queue ! ximagesink
# gst-launch-1.0 videotestsrc pattern=ball ! video/x-raw,height=100,width=100 ! av1enc ! av1dec ! identity silent=true ! autovideosink sync=false -v
# gst-launch-1.0 rtspsrc location=rtsp://admin:Obodroid@192.168.1.23/media/video1 ! rtph264depay ! h264parse ! avdec_h264 ! queue ! autovideosink

# python3 webrtc_recvonly.py 1 --server=ws://192.168.1.61:8443