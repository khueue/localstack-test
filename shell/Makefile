__default:
	@ cat ./Makefile

SHELL=/usr/bin/env bash

# NOTE: The localstack_default network should be created beforehand by
# docker compose.

cmd := bash --login
shell: IMAGE_TAG=localstack-test-shell
shell:
	docker build \
		--tag $(IMAGE_TAG) \
		--file ./Dockerfile \
		./
	docker run --interactive --tty --rm --init \
		--mount type="bind",source="$(PWD)/",target="/workdir/",consistency="delegated" \
		--mount type="bind",source="$(PWD)/../terraform/",target="/terraform/",consistency="delegated" \
		--network localstack_default \
		--workdir /workdir/ \
		$(IMAGE_TAG) \
		bash -c "$(cmd)"
