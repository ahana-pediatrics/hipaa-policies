desc "Build static site to build directory"
task :build do
  status = system("bundle exec middleman build --clean")
  puts status ? "OK" : "FAILED"
end

desc "Run the middleman server"
task :run do
  system("middleman server -p 2113")
end

desc "Watch and compress Sass"
task :sass do
  system("cd source/assets/css && sass --watch styles.scss:styles.css --style compressed")
end

desc "Run a simple web server within the build directory"
task :serve_static do
  system("cd build && python -m http.server 8888")
end

desc "Deploy site to AWS"
task :deploy do
  system("aws s3 sync build s3://policy.ahana.health")
  system("aws cloudfront create-invalidation --distribution-id E10IGBL3RQGLLT --paths /\\*")
end