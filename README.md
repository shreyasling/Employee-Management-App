# Employee Management App
This is a Ruby on Rails based web application for managing employee data.

## Installation

Before you can deploy the Employee Management App, you need to make sure that you have the following dependencies installed on your machine:

- Ruby (3.0.5)
- Mysql or Mariadb
- yarn
- nodejs

-Clone the repository to your local machine.
```bash
git clone https://github.com/shreyasling/Employee-Management-App.git
cd src
```
Create a docker file named(Dockerfile)
-copy this to your dockerfile by any text editior
```bash
FROM ruby:3.0.5

ENV RAILS_ROOT /project

RUN apt-get update && \
  apt-get install -y \
  build-essential \
  nodejs \
  yarn \
  libpq-dev && \
  mkdir -p $RAILS_ROOT && \
  apt-get clean autoclean && \
  apt-get autoremove -y && \
  rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log
WORKDIR $RAILS_ROOT

COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock
RUN gem install bundler
RUN bundle install
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list


COPY package.json package.json
COPY yarn.lock yarn.lock

COPY . .

EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
```
SCREENSHOT:
![a](https://github.com/shreyasling/Employee-Management-App/blob/shrey/Screenshot%20from%202023-04-08%2016-04-08.png)

Configure database settings at `config/database.yml`.
Build Docker image by running this command:
```bash
sudo docker build -t employee-management-app .
```
How it looks:
![b](https://github.com/shreyasling/Employee-Management-App/blob/shrey/Screenshot%20from%202023-04-08%2016-03-00.png)

Run Docker container by running this command:
```bash
sudo docker run -p3000:3000 employee-management-app
```
How it looks:
![c](https://github.com/shreyasling/Employee-Management-App/blob/shrey/Screenshot%20from%202023-04-08%2016-05-12.png)


After starting the server, you can access the web application by visiting http://localhost:3000 in your web browser.
![D](https://github.com/shreyasling/Employee-Management-App/blob/shrey/Screenshot%20from%202023-04-08%2012-31-59.png)


``


