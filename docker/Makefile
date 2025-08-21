# parameters
DOCKER ?= docker
DOCKER_BUILD_TARGET ?= compiler-dev-arm
DOCKER_IMAGE_NAME ?= compiler-dev-arm
DOCKER_BUILD_OPTS ?=

# directories
TOP_DIR := $(shell pwd)
REPO_DIR := $(realpath $(TOP_DIR)/..)
KOOPAC_DIR := $(REPO_DIR)/koopac
KOOPAC_DIR_NAME := koopac
KOOPA_DIR := $(REPO_DIR)/koopa
KOOPA_DIR_NAME := koopa
SYSYRTLIB_DIR := $(REPO_DIR)/sysy-runtime-lib
SYSYRTLIB_DIR_NAME := sysy-runtime-lib
CASES_DIR := $(REPO_DIR)/compiler-dev-test-cases
CASES_DIR_NAME := compiler-dev-test-cases

# files
KOOPAC_SRCS := $(shell find $(KOOPAC_DIR)/src -name "*.rs")
KOOPAC_SRCS += $(KOOPAC_DIR)/Cargo.toml
KOOPA_SRCS := $(shell find $(KOOPA_DIR)/src -name "*.rs")
KOOPA_SRCS += $(KOOPA_DIR)/Cargo.toml
SYSYRTLIB_SRCS := $(shell find $(SYSYRTLIB_DIR)/src -name "*.[ch]")
AUTOTEST_SRC := $(REPO_DIR)/autotest/autotest
CASES_SRC := $(shell find $(CASES_DIR) -type f \( -name "*.c" -o -name "*.in" -o -name "*.py" \))

# targets
KOOPAC_NAME := koopac.tar.gz
KOOPAC := $(TOP_DIR)/$(KOOPAC_NAME)
AUTOTEST_NAME := autotest
AUTOTEST := $(TOP_DIR)/$(AUTOTEST_NAME)
KOOPA_NAME := koopa.tar.gz
KOOPA := $(TOP_DIR)/$(KOOPA_NAME)
SYSYRTLIB_NAME := sysy-runtime-lib.tar.gz
SYSYRTLIB := $(TOP_DIR)/$(SYSYRTLIB_NAME)
CASES_NAME := compiler-dev-test-cases.tar.gz
CASES := $(TOP_DIR)/$(CASES_NAME)

BUILD_CONTEXT := $(TOP_DIR)/update-alternatives-clang.sh
BUILD_CONTEXT += $(KOOPAC) $(AUTOTEST) $(KOOPA) $(SYSYRTLIB) $(CASES)

# docker
DOCKER_BUILD_FLAGS := --target $(DOCKER_BUILD_TARGET) -t $(DOCKER_IMAGE_NAME)
DOCKER_BUILD_FLAGS += $(DOCKER_BUILD_OPTS) --build-arg KOOPAC=$(KOOPAC_NAME)
DOCKER_BUILD_FLAGS += --build-arg AUTOTEST=$(AUTOTEST_NAME)

.PHONY: docker clean

docker: $(TOP_DIR)/Dockerfile $(BUILD_CONTEXT)
	$(DOCKER) build $(DOCKER_BUILD_FLAGS) .

clean:
	-rm $(KOOPAC) $(AUTOTEST)

$(KOOPAC): $(KOOPAC_SRCS)
	cd .. && git archive --format=tar.gz -o $@ HEAD:$(KOOPAC_DIR_NAME)

$(AUTOTEST): $(AUTOTEST_SRC)
	cp $^ $@

$(KOOPA): $(KOOPA_SRCS)
	cd $(KOOPA_DIR) && git archive --format=tar.gz -o $@ HEAD

$(SYSYRTLIB): $(SYSYRTLIB_SRCS)
	cd $(SYSYRTLIB_DIR) && git archive --format=tar.gz -o $@ HEAD

$(CASES): $(CASES_DIR)
	cd $(CASES_DIR) && git archive --format=tar.gz -o $@ HEAD
