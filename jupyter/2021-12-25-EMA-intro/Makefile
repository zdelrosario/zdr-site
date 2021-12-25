SRC := $(wildcard *.ipynb)
STEM := $(subst .ipynb,,$(SRC))
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
	find $*_files -maxdepth 1 | grep png | xargs -I{} convert {} -background white -alpha remove -alpha off {}
	cp -f $*_files/* ../../static/media/$*_files/.
	# Move to post
	mkdir -p ../../content/post/${DIR}
	mv -f index.md ../../content/post/${DIR}/.
	find $*_files -maxdepth 1 -type f | grep png | head -1 | xargs -I{} cp {} ../../content/post/${DIR}/featured.png

add:
	# Add post files
	git add ../../content/post/${DIR}
	git add ../../static/media/${STEM}_files

clean:
	rm ${MD}
	rm -fr *_files
