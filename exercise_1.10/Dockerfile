FROM node

EXPOSE 5000

WORKDIR /
RUN ["git", "clone", "https://github.com/docker-hy/frontend-example-docker.git"]
WORKDIR /frontend-example-docker
RUN ["npm", "install"]

# This is for running exercise >= 1.12
ENV API_URL=http://stream:8000

ENTRYPOINT ["npm"]
CMD ["start"]
