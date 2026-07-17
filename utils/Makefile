# Default values
default_server := Test
default_key := /keys/MyKey.pem

CONFIG_FILE := servers.config

# Require server name
server ?= $(error Server name must be specified. Example: make connect server=tbhl-hf-apache-web-a-0)

.PHONY: connect connect_to show

# Main target
connect:
	@$(MAKE) connect_to server=$(server)

# Connect to server
connect_to:
	@echo "Connecting to server $(server)"
	$(eval SERVER_DETAILS := $(shell grep "^$(server)," $(CONFIG_FILE)))

	@if [ -z "$(SERVER_DETAILS)" ]; then \
		echo "Server '$(server)' not found in $(CONFIG_FILE)"; \
		exit 1; \
	fi

	$(eval SERVER := $(shell echo "$(SERVER_DETAILS)" | cut -d',' -f1))
	$(eval IP := $(shell echo "$(SERVER_DETAILS)" | cut -d',' -f2))
	$(eval SSH_KEY := $(shell echo "$(SERVER_DETAILS)" | cut -d',' -f3))
	$(eval USER := $(shell echo "$(SERVER_DETAILS)" | cut -d',' -f4))

	@echo "Using server : $(SERVER)"
	@echo "IP          : $(IP)"
	@echo "User        : $(USER)"
	@echo "SSH Key     : $(SSH_KEY)"

	@ssh \
		-o ServerAliveInterval=30 \
		-o ServerAliveCountMax=3 \
		-o ConnectTimeout=10 \
		-i ./keys/$(SSH_KEY) \
		$(USER)@$(IP)

# Show parsed values
show:
	$(eval SERVER_DETAILS := $(shell grep "^$(server)," $(CONFIG_FILE)))
	$(eval STR := $(subst ,, ,$(SERVER_DETAILS)))
	@echo "SERVER_DETAILS = $(SERVER_DETAILS)"
	@echo "STR = $(STR)"
