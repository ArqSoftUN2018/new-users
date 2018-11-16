FROM ruby:2.5.0
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs 
# Set an environment variable where the Rails app is installed to inside of Docker image
ENV RAILS_ROOT /var/www/users
RUN mkdir -p $RAILS_ROOT 
# Set working directory
WORKDIR $RAILS_ROOT
# Setting env up
ENV RAILS_ENV='production'
ENV RACK_ENV='production' 
# Adding gems
COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock
COPY api_authentication api_authentication
#RUN bundle install --jobs 20 --retry 5 --without development test 
RUN bundle install --without development test
# Adding project fil es
#RUN mkdir -p /var/www/users/api_authentication
COPY . .
EXPOSE 3000
CMD ["bundle", "exec", "puma", "-C", "config/puma.rb"]