FROM node

EXPOSE 8000

WORKDIR /
RUN ["git", "clone", "https://github.com/docker-hy/backend-example-docker.git"]
WORKDIR /backend-example-docker
RUN ["npm", "install"]

ENTRYPOINT ["npm"]
CMD ["start"]
