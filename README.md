# Blog Address

<https://tyler-yox.github.io/blog/>

# Develop
## LMDE
```
# First-time Setup
sudo apt-get install ruby-full build-essential ruby-bundler
gem install jekyll bundler
export GEM_HOME="$HOME/.local/share/gem/ruby/3.3.0"
export PATH="$HOME/.local/share/gem/ruby/3.3.0/bin:$PATH"
source ~/.bashrc

# Serve
bundle update
bundle exec jekyll serve

# Test
google-chrome --disable-web-security --user-data-dir="/tmp/chrome_dev"
# Go to http://localhost:4000/
```

# Must Modify

## 1.swiftype

This service provides the on-site search function.

Service address: <https://swiftype.com/>.

Documentation: <https://swiftype.com/documentation/site-search/crawler-quick-start/>

After the setup is complete， you need to modify the `swiftype.searchId` in `_config.yml`.

In your swiftype engine, go to `Install Search`, you will find the `swiftype.searchId`.

```html
<script type="text/javascript">
...
...
  _st('install','swiftype.searchId','2.0.0');
</script>
```

## 2.gitalk

This service provides the comment function.

Service address： <https://github.com/gitalk/gitalk>.

After the setup is complete， you need to modify the `comment`  in `_config.yml`.
