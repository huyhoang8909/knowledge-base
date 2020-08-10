# Rails

## rails console
RAILS_ENV=staging bundle exec rails c
rails c -e staging
bundle exec cap production deploy

## start delay jobs
RBENV_ROOT=~/.rbenv RAILS_ENV=production RBENV_VERSION=2.x ~/.rbenv/bin/rbenv exec bundle exec bin/delayed_job start
