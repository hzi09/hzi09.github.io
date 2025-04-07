source "https://rubygems.org"

# GitHub Pages와 호환되는 버전 사용
gem "github-pages", group: :jekyll_plugins
gem "minimal-mistakes-jekyll"

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-sitemap"
  gem "jekyll-include-cache"
  gem "jekyll-paginate"
  gem "jekyll-gist"
end

# 추가 의존성
gem "kramdown-parser-gfm"
gem "faraday-retry"
gem "base64"

# Windows와 JRuby는 이 의존성이 필요함
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds,
# newer versions of the gem do not have a Java counterpart
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]