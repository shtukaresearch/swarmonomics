TARGET ?= ./target
NAME = swarmonomics-2025-05
ENV_NAME = swarmonomics-build
INVOKER ?= podman run --rm -v $$(pwd):/tex:Z -v $$(pwd)/../common:/tex/common:Z -w /tex $(ENV_NAME)

all: $(TARGET)/$(NAME).pdf

$(TARGET):
	mkdir -p $@

$(TARGET)/$(NAME).pdf: $(NAME).tex document.tex | $(TARGET)
	$(INVOKER) lualatex -synctex=1 -interaction=batchmode -output-directory=$(TARGET) $(NAME)

build-once: | $(TARGET)
	$(INVOKER) lualatex -synctex=1 -interaction=batchmode -output-directory=$(TARGET) $(NAME)

debug: | $(TARGET)
	$(INVOKER) lualatex -synctex=1 -output-directory=$(TARGET) $(NAME)

clean: | $(TARGET)
	rm $(TARGET)/*