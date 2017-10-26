# TODO: Change it to registry lcoation.
IMAGE_FRONT ?= iberdinsky/yarn-swiss-knife


# TODO: parse package.json to get "name" and use as NAME
# https://gist.github.com/DarrenN/8c6a5b969481725a4413
NAME = pandemia


# We need to have extra shared volume.
EXTRA_SHARED_VOL = -v $(shell pwd)/../themes/newco:/themes/newco

# TODO: Add abylity to use external Dockerfile.
# Dockerfile location.
FILE = Dockerfile

front = docker run --rm  -it -v $(shell pwd):/work $(EXTRA_SHARED_VOL) $(IMAGE_FRONT):$(NAME) ${1}

all: | check

check:
	# TODO: add cmparision between local package.json and docker one.
	# If they are not equal or docker not exists rebuild/push.
	if [ -a package.json ] ; \
	then \
	     make build ; \
			 make push ; \
	fi;
	make front

front:
	@echo "Building front tasks..."
	$(call front, gulp)

exec:
	$(call front, sh)

task:
	$(call front, npm run)

clean:
	rm -rf node_modules


build:
	docker build -t $(IMAGE_FRONT):$(NAME) --file=$(FILE) .

push:
	docker push $(IMAGE_FRONT):$(NAME)


# TODO: Add task with universal image.
