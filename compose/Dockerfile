FROM golang:1.19
ARG GIT_AUTH_TOKEN

# Install Git
RUN apt-get update
RUN apt-get install git

# Clone Git Repository
WORKDIR /tmp
RUN git clone https://${GIT_AUTH_TOKEN}@github.com/mmaaskant/gro-crop-scraper.git
WORKDIR /tmp/gro-crop-scraper
RUN go build -o=/bin/gro-crop-scraper
RUN rm -rf /tmp/gro-crop-scraper

# By default scrape all websites
CMD ["gro-crop-scraper"]