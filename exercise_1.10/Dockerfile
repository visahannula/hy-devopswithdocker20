FROM node

EXPOSE 5000

WORKDIR /
RUN ["git", "clone", "https://github.com/docker-hy/frontend-example-docker.git"]
WORKDIR /frontend-example-docker
RUN ["npm", "install"]

ENTRYPOINT ["npm"]
CMD ["start"]