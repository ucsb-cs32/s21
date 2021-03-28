# github.com/ucsb-cs32/f20

Jekyll-based website for CS32, Spring 2021

Website: <https://ucsb-cs32.github.io/s21/>

The theme currently being used can be find in the jekyll-theme value
in `_config.yml`

The navigation is set by the values in `_data/navigation.yml`

To test locally:
* One time setup:
    * `git clone` the repo
    * Install rvm (the Ruby version manager)
    * Run `./setup.sh` to install correct ruby version, bundler version, and bundle the gems
* From then on, to test the site locally:
    * Run `./jekyll.sh`
    * Point browser to <https://localhost:4000/s21/>
