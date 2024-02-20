# Please choose from the below set of Docker commands to complete your Dockerfile:

# COPY Copy files and directories from the host machine (where the Docker build is being performed) into the Docker image being built
# RUN Execute commands during the image build process
# ADD used in a Dockerfile to copy files and directories from the build context (usually the directory where your Dockerfile is located) into the Docker image being built. It has a similar function to COPY, but it also supports URLs and automatically extracts compressed files.
# EXPOSE informs Docker that the container listens on specific network ports at runtime. It does not actually publish the ports, but rather serves as a documentation mechanism for the ports that are intended to be exposed.
# FROM Is used to specify the base image upon which the subsequent instructions will be based. It is always the first non-comment instruction in a Dockerfile.
# CMD Is used to specify the default command that should be executed when a container is run from the Docker image. It sets the command and any arguments that will be passed to the container's entry point
# PUSH is used to push (upload) Docker images to a container registry. This makes the images available for use by others, such as team members or servers
# PULL is used to pull (download) Docker images from a container registry to your local machine. This allows you to obtain images that you want to run as containers on your system.
# WORKDIR is used to set the working directory for any subsequent RUN, CMD, ENTRYPOINT, COPY, and ADD instructions. This instruction can be used to set a default directory for commands executed within the container.
# export MY_NAMESPACE=sn-labs-$pedromirand1
# docker build . -t us.icr.io/$MY_NAMESPACE/guestbook:v1
# docker push us.icr.io/$MY_NAMESPACE/guestbook:v1
# kubectl apply -f deployment.yml
# kubectl autoscale deployment guestbook --cpu-percent=5 --min=1 --max=10
# kubectl get hpa guestbook
# kubectl apply -f deployment.yml
# docker build . -t us.icr.io/$MY_NAMESPACE/guestbook:v1 && docker push us.icr.io/$MY_NAMESPACE/guestbook:v1
# kubectl rollout undo deployment/guestbook --to-revision=1


FROM golang:1.15 as builder
RUN go get github.com/codegangsta/negroni
RUN go get github.com/gorilla/mux 
RUN go get github.com/xyproto/simpleredis/v2
COPY main.go .
RUN go build main.go

FROM ubuntu:18.04

COPY --from=builder /go//main /app/guestbook
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

WORKDIR /app
CMD ["./guestbook"]
EXPOSE 3000
