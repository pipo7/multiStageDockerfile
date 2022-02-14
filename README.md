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
