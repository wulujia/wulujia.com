require 'rake'

desc 'Default: Server'
task :default => :server

desc "server"
task :server do
  system "start http://localhost:4000/"
  system "jekyll serve --watch"
end

# rake ci msg="message"
desc "commit"
task :ci do
  system "rake tags"
  message = ENV['msg'] || "update"
  system "git commit -a -m \"#{message}\""
  system "git push"
end

desc 'Generate tag pages'
task :tags do
  puts "Generating tag pages..."
  require 'jekyll'
  
  options = Jekyll.configuration({})
  site = Jekyll::Site.new(options)
  site.read_posts('')
  site.categories.sort.each do |category, posts|
    html = ''
    html << <<-HTML
---
layout: default
title: Thoughts by rafeca
---
<header>
  <h1><a class="fadedlink" href="/" title="Home">&laquo;</a> {{ site.title }}</h1>
  <h2>Posts in category "#{category}"</h2>
</header>

<ul>
  {% for post in site.categories.#{category} %}
    {% include post.html %}
  {% endfor %}
</ul>
    HTML
    File.open("tag/#{category}.html", 'w+') do |file|
      file.puts html
    end
    puts "tag/#{category}.html generated!"
  end
  puts 'Done!'
end
