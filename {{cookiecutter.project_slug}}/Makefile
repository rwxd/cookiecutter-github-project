PROJECT_NAME := "{{ cookiecutter.project_slug }}"
{% if cookiecutter.project_type == "go" %}
PKG := "github.com/rwxd/$(PROJECT_NAME)"
PKG_LIST := $(shell go list ${PKG}/...)
GO_FILES := $(shell find . -name '*.go' | grep -v _test.go)
{% endif %}
help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

setup: ## Setup required things
	{% if cookiecutter.project_type in ["python", "ansible"] %}
	@python3 -m pip install -r requirements.txt
	{% endif %}
	@python3 -m pip install -r requirements-dev.txt
	{% if cookiecutter.project_type == "go" %}
	@go get -v -d ./...
	{% endif %}
