# Run as 
go run demo.go
# OR compile and run the binary
go vet demo.go && go fmt demo.go && golangci-lint run --timeout 5m  \
&& env GOOS=linux GOARCH=amd64 go build .

# OR run as container , for this we hae 3 ways to generate image via Dockerfiles
Dockerfile.test1 rename to Dockerfile  and run 
docker build -t distrolessimage .
# OR
Dockerfile.test2 rename to Dockerfile  and run 
docker build -t distrolessDebianDebugimage .
# OR
Dockerfile.test3 rename to Dockerfile  and run 
docker build -t scratchimage .# multiStageDockerfile

# Check that final image size is far less than overall image 
# You can test by running a particular stage and compare image sizes for example , in Dockerfile.test3
 docker build --target buildstage1 -t myimage:latest .
 VS
 docker build --target buildstage2 -t myfinalimag2:latest .


 # another example:
 You can pick up where a previous stage left off by referring to it when using the FROM directive. For example:

# syntax=docker/dockerfile:1
FROM alpine:latest AS builder
RUN apk --no-cache add build-base

FROM builder AS build1
COPY source1.cpp source.cpp
RUN g++ -o /binary source.cpp

FROM builder AS build2
COPY source2.cpp source.cpp
RUN g++ -o /binary source.cpp
