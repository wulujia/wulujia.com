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
  message = ENV['msg'] || "update blog"
  system "rake tags"
  system "git add ."
  system "git commit -a -m \"#{message}\""
  system "git push origin gh-pages"
end

desc 'Generate tags pages'
task :tags do
  puts "Generating tags pages..."
  require 'jekyll'
  
  options = Jekyll.configuration({})
  site = Jekyll::Site.new(options)
  site.read_posts('')
  site.tags.sort.each do |tag, posts|
    html = ''
    html << <<-HTML
---
layout: default
title: wulujia.com
---
<header>
  <h1><a class="fadedlink" href="/" title="Home">&laquo;</a> {{ site.title }}</h1>
  <h2>标签 #{tag} 下的内容：</h2>
</header>

<ul>
  {% for post in site.tags.#{tag} %}
    <li><span>{{ post.date | date:"%Y-%m-%d" }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
    HTML
    File.open("tags/#{tag}.html", 'w+') do |file|
      file.puts html
    end
    puts "tags/#{tag}.html generated!"
  end
  puts 'Done!'
end
