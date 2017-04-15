require 'rake/clean'
CLEAN.class

desc 'default task html'
task :default => [:html]

desc 'build html book format'
task :html do
  puts 'Converting to HTML...'
  `bundle exec asciidoctor -a stylesheet=./themes/html/asciidoctor.css book.asc`
  puts ' -- HTML output at book.html'
end
CLOBBER.include('book.html')

desc 'build pdf book format'
task :pdf do
  puts 'Converting to PDF... (this one takes a while)'
  `bundle exec asciidoctor-pdf -a pdf-style=themes/pdf/default-theme.yml book.asc 2>/dev/null`
  puts ' -- PDF  output at book.pdf'
end
CLOBBER.include('book.pdf')

desc 'build epub book format'
task :epub do
  puts 'Converting to EPub...'
  `bundle exec asciidoctor-epub3 book.asc`
  puts ' -- Epub output at book.epub'
end
CLOBBER.include('book.epub')

desc 'build mobi book format'
task :mobi do
  puts 'Converting to Mobi (kf8)...'
  `bundle exec asciidoctor-epub3 -a ebook-format=kf8 book.asc`
  puts ' -- Mobi output at book.mobi'
end
CLOBBER.include('book.mobi')

desc 'build basic book formats'
task :build => [:html, :pdf, :epub, :mobi] do
  # run the tests
end
