FROM node

EXPOSE 8000

WORKDIR /
RUN ["git", "clone", "https://github.com/docker-hy/backend-example-docker.git"]
WORKDIR /backend-example-docker
RUN ["npm", "install"]

# This is for running exercise >= 1.12
ENV FRONT_URL=http://stream:8088

ENTRYPOINT ["npm"]
CMD ["start"]
