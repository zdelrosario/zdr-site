SRC := $(wildcard *.ipynb)
MD := $(subst ipynb,md,$(SRC))
mkfile_path := $(abspath $(lastword $(MAKEFILE_LIST)))
DIR := $(notdir $(patsubst %/,%,$(dir $(mkfile_path))))

all: ${MD}

%.md: %.ipynb
	# Render to markdown
	jupyter nbconvert --to markdown $<
	# Concatenate the header and rendered notebook
	cat top.md $@ > index.md
	# Move the images to static
	mkdir -p ../../static/media/$*_files
	cp -f $*_files/* ../../static/media/$*_files/.
	# Move to post
	mkdir -p ../../content/post/${DIR}
	mv -f index.md ../../content/post/${DIR}/.
	find $*_files -maxdepth 1 -type f | grep png | head -1 | xargs -I{} cp {} ../../content/post/${DIR}/featured.png

clean:
	rm ${MD}
	rm -fr *_files
