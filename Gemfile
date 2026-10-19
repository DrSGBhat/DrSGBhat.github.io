source "https://rubygems.org"

# Gems for building the site on your own computer:
#
#     bundle install
#     bundle exec jekyll serve
#
# GitHub Pages builds the live site with its own fixed set of gems and
# ignores this file. The versions below match what it uses (github-pages 232),
# so local builds look the same as the live site.
#
# This lists Jekyll and the plugins directly instead of using the umbrella
# "github-pages" gem. That gem pins jekyll-remote-theme, which holds rubyzip
# below the fix for CVE-2026-85396, and this site doesn't use a remote theme.

gem "jekyll", "3.10.0"
gem "kramdown-parser-gfm", "1.1.0"

# Plugins named under `gems:` in _config.yml, plus the sitemap
group :jekyll_plugins do
  gem "jekyll-feed", "0.17.0"
  gem "jekyll-gist", "1.5.0"
  gem "jekyll-paginate", "1.1.0"
  gem "jekyll-redirect-from", "0.16.0"
  gem "jekyll-sitemap", "1.4.0"
end

# No longer part of Ruby's standard library on recent Ruby versions
gem "base64"
gem "bigdecimal"
gem "logger"

gem "wdm", "~> 0.1.0" if Gem.win_platform?
