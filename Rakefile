desc "Build a pdf version as gitref.pdf"
task 'gitref.pdf' => '_site' do
  `rm -rf _site; jekyll`
  pages = File.read('_site/about.html').scan(/<h3><a href=['"]([^'"]+)/).flatten.map { |f| "_site/#{f}/index.html" }
  pages.pop
  pages << 'gitref.pdf'
  system(%q{find _site -name '*.html' | xargs sed -ie 's/href="\/css/href="..\/..\/css/g'})
  system(%q{find _site -name '*.html' | xargs sed -ie 's/layout.css" media="screen" \/>/layout.css" media="screen" \/><link rel="stylesheet" type="text\/css" href="..\/..\/css\/print.css" media="screen" \/>/'})
  sh 'wkhtmltopdf', '-b', '--toc-depth', '1', '--header-spacing', '5', '--user-style-sheet', 'file://./css/print.css', *pages
end

task :default => 'gitref.pdf'
