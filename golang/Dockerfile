# First stage: Build the Go application
FROM tetafro/golang-gcc AS builder

WORKDIR /go/fullcycle

COPY . .

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags="-s -w" -o fullcycle fullcycle.go

# Second stage: Create a smaller final image
FROM scratch

WORKDIR /go/fullcycle

# Copy the built binary from the builder stage
COPY --from=builder /go/fullcycle/fullcycle .

# Run the compiled binary
ENTRYPOINT ["./fullcycle"]
