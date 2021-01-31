FROM alpine:3.13.0
RUN apk add --no-cache stress-ng
RUN addgroup -S appgroup -g 1000 && adduser -S appuser -G appgroup -u 1000
USER 1000
WORKDIR /home/appuser

CMD ["sleep", "infinity"]
