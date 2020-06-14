# To build the project

First you have to clone or update the repo from Github.

Then there are two ways to build the static files:

1. **Manual method:** This method might require some OS specific libraries to be installed separately, especially ones that are related to image manipulation. But after cloning run:
```sh
npm install
```
If it ran without errors, then run:
```sh
npm run build
```

2. **Docker method:** This will install all the dependencies inside Docker, so no need to do any other manual setup:
```sh
docker-compose up --build
```
After the image is built and running, in another command-line tab run the following command:
```sh
docker exec -it \
$(docker ps -f name=gridsome_issue_650_test --format "{{.ID}}") \
node ../node_modules/.bin/gridsome build
```
