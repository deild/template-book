require 'rake/clean'
CLEAN.class

desc 'default task html'
task :default => [:html]

desc 'prepare build'
 task :prebuild do
   Dir.mkdir 'images' unless Dir.exists? 'images'
   Dir.glob("book/**/*.jpg").each do |image|
     FileUtils.copy(image, "images/" + File.basename(image))
     CLEAN.include("images/" + File.basename(image))
   end
   Dir.glob("book/**/*.png").each do |image|
     FileUtils.copy(image, "images/" + File.basename(image))
     CLEAN.include("images/" + File.basename(image))
   end
 end

desc 'build html book format'
task :html => [:prebuild] do
  puts 'Converting to HTML...'
  `bundle exec asciidoctor -a revdate=$(date +%Y-%m-%d) -a stylesheet=./themes/html/custom.css book.asc`
  puts ' -- HTML output at book.html'
end
CLOBBER.include('book.html')

desc 'build pdf book format'
task :pdf => [:prebuild] do
  puts 'Converting to PDF... (this one takes a while)'
  `bundle exec asciidoctor-pdf -a revdate=$(date +%Y-%m-%d) -a pdf-style=./themes/pdf/default-theme.yml book.asc 2>/dev/null`
  puts ' -- PDF  output at book.pdf'
end
CLOBBER.include('book.pdf')

desc 'build epub book format'
task :epub => [:prebuild] do
  puts 'Converting to EPub...'
  `bundle exec asciidoctor-epub3 -a revdate=$(date +%Y-%m-%d) book.asc`
  puts ' -- Epub output at book.epub'
end
CLOBBER.include('book.epub')

desc 'build mobi book format'
task :mobi => [:prebuild] do
  puts 'Converting to Mobi (kf8)...'
  `bundle exec asciidoctor-epub3 -a revdate=$(date +%Y-%m-%d) -a ebook-format=kf8 book.asc`
  puts ' -- Mobi output at book.mobi'
end
CLEAN.include('book-kf8.epub')
CLOBBER.include('book.mobi')

desc 'build basic book formats'
task :build => [:html, :pdf, :epub, :mobi] do
  # run the tests
end
