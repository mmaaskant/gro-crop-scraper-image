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

# An image is build only through docker build, which can be ran in a CI/CD pipeline.
# For so, even with git setup that would pull the latest version; the manual creation of the image is tagged and cached
# Thus to update the image, you'd either would have to do so manually or setup CI/CD bound to a new release event which will then automatically create images

# For now, this repo will serve as a manual tool to create images; for so it has to do the following:
# - Pull project for Git, either through Tar (No git, no Auth) or Git clone (Git, Auth)
# - Build an artifact that matches the Go base image
# - Delete the project files, and move the artifact to bin

# The artifact can then be ran using a command within the Kubernetes deployment job configuration
# This configuration can then either target all available scrapers, or a targeted scraper using the command + its flags

# TODO: Finish this image builder, create a helm chart for the mongoDB deployment + Cron job for scraper
# TODO: Upgrade these manual images to a Github action CI/CD/Package setup where once a new release is ran, an image is automatically build + tagged