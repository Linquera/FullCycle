FROM golang:1.7.3 as builder
WORKDIR /go/src/github.com/linquera/FullCycle/Docker/DesafioGo
RUN go get -d -v golang.org/x/net/html  
COPY app.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM gruebel/upx:latest as upx
COPY --from=builder /go/src/github.com/linquera/FullCycle/Docker/DesafioGo/app /app.org
RUN upx --best --lzma -o /app /app.org

FROM scratch
WORKDIR /root/
COPY --from=upx /app .
CMD ["./app"] 