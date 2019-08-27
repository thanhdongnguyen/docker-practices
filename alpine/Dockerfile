FROM alpine:3.10.1

RUN apk add --update && \
	apk add bash curl wget git vim tmux  && \
	rm -rf /var/cache/apk/*

CMD ["/bin/bash"]