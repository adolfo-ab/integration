REGISTRY ?= quay.io/oc-mirror/oc-mirror-dev
RUNTIME ?= podman
OUTPUT = _output

all: build
.PHONY: all

build:
	go run ./cmd/build-catalogs
.PHONY: build

push: build
	@for dir in $(OUTPUT)/test-catalog-*/; do \
		name=$$(basename "$$dir"); \
		echo "Building $$name"; \
		$(RUNTIME) build --format=docker -t "$(REGISTRY):$$name" \
			-f "$(OUTPUT)/$$name.Dockerfile" $(OUTPUT); \
		$(RUNTIME) push --format=docker "$(REGISTRY):$$name"; \
	done
.PHONY: push

clean:
	rm -rf $(OUTPUT)
.PHONY: clean
