desc "Publicar en GitHub los apuntes de PL"
task :default do
  sh "git ci -am 2020 && git push"
end

desc "bundle exec jekyll serve"
task :serve do
  sh "bundle exec jekyll serve --no-watch --incremental"
end

desc "sytws: bundle exec jekyll serve"
task :serve do
  sh "git pull origin master"
  sh "bundle exec jekyll serve -H 10.6.128.216 -P 8080"
end
