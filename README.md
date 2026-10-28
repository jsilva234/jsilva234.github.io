# Local Setup

```bash
brew install rbenv ruby-build openssl@3 # ruby version manager + openssl 3
echo 'eval "$(rbenv init - zsh)"' >> ~/.zshrc && source ~/.zshrc

# 3.3.x on purpose: GitHub Pages builds with 3.3, and 3.4+ may break the old github-pages gem
# openssl@3 on purpose: ruby-build picks openssl@4 by default, which gave a broken Ruby 3.3
RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@3)" rbenv install 3.3.13
rbenv local 3.3.13          # writes .ruby-version in this repo

gem install bundler:2.4.10
bundle install

bundle exec jekyll serve
```

Open http://localhost:4000
