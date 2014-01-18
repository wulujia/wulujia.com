require 'rake'

desc 'Default: Server'
task :default => :server

desc "server"
task :server do
  system "rake tags"
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
<head>
  <h1><a href="/">{{ site.title }}</a></h1>
</head>

<div class="clearfix">
	{% for category in site.categories %}
	<a href="/categories/{{category[0]}}.html">{{category[0]}} <span class="badge">{{category[1].size}}</span></a>&nbsp;&nbsp;&nbsp;       
	{% endfor %}
</div>

<h2><span>标签为 #{tag} 的文章</span></h2>
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
