#!/usr/bin/rake -T

# This Rakefile is used for building the presentation from the modified presentation base.

require 'erb'
require 'find'
require 'rake/clean'

### General Presentation Information ###
TITLE = 'Distributed OpenSCAP Compliance Validation with MCollective'
DESCRIPTION = 'A presentation covering a custom MCollective Plugin written for scanning systems with OpenSCAP'
AUTHOR = 'Trevor Vaughan - Onyx Point, Inc.'
GLOBAL_HEADER = 'MCollective OpenSCAP Validation'
### End General Presentation Information ###

### Slide Management ###

FIRST_SLIDE = '00'
LAST_SLIDE = '999'

# A template for creating new slides.
SLIDE_TEMPLATE = <<-EOM
<section>
</section>
EOM

### End Slide Management ###

BASE_DIR = File.dirname(__FILE__)
BUILD_DIR = "#{BASE_DIR}/build"
SLIDE_DIR = "#{BASE_DIR}/slides"
REVEAL_JS_SRC = 'https://github.com/onyxpoint/reveal.js'

CLOBBER.include(
  BUILD_DIR,
  'node.js'
)

def sorted_slides(slide_dir)
  Dir.chdir(slide_dir) do
    Dir.glob('*').sort_by{|f| File.basename(f,'.md').split('_').first.to_i}.each do |x|
      if x =~ /\.md$/
        yield(x)
      end
    end
  end
end

# This can handle nested slides, unfortunately the header mods by Ciges
# currently cause issues with vertical scrolling.
def build_slides(slides)
  sorted_slides(Dir.pwd) do |slide|
    subdir = File.basename(slide,'.md')
    if @use_subsections and File.directory?(File.basename(slide,'.md'))
      has_subsections = true
      slides << '<section>'
    end

    if slide =~ /\.md$/
      slides << '<section data-markdown>'
      slides << '<script type="text/template">'
      slides << File.read(slide).chomp
      slides << '</script>'
      slides << '</section>'
    end

    if File.directory?(subdir)
      Dir.chdir(subdir) do
        build_slides(slides)
      end
    end

    if has_subsections
      slides << '</section>'
    end
  end

  slides.join("\n")
end

desc "Build the presentation based on #{REVEAL_JS_SRC}

  * :one_level - Don't use sub-sections"
task :build,[:one_level] do |t,args|
  directory BUILD_DIR

  args.with_defaults(
    :one_level => false
  )

  @use_subsections = !(args.one_level)

  if not File.directory?(BUILD_DIR)
    sh %{git clone #{REVEAL_JS_SRC} #{BUILD_DIR}}
  else
    Rake::Task['clean'].invoke
  end

  Dir.chdir(BUILD_DIR) do
    FileUtils.mv('LICENSE','LICENSE_reveal.js')
  end

  slides = []
  Dir.chdir(SLIDE_DIR) do
    slides = build_slides(slides)
  end

  # Build the index.html file
  File.open('index.html','w') { |fh|
    fh.puts(ERB.new(File.read('index.html.erb'),nil,'-').result(binding))
  }

  sh %{tar --exclude-vcs --exclude='node.js' --exclude='build' --exclude='*.erb' -cf - . | tar -C build -xf -}
end

desc "Reset the bulid directory to a clean state"
task :clean do
  Dir.chdir(BUILD_DIR) do
    puts "== In #{BUILD_DIR} =="
    sh %{git clean -qdf}
    sh %{git reset -q --hard HEAD}
    puts "== Leaving #{BUILD_DIR} =="
  end

  Find.find('.') do |f|
    base_file = File.basename(f,'.erb')
    FileUtils.rm(base_file) if File.exist?(base_file) and f =~ /\.erb$/
  end
end

desc "Host the slides in a local Node.js"
task :host do
  FileUtils.mkdir('node.js') unless File.directory?('node.js')

  Dir.chdir('node.js') do
    sh %{wget -q -nH --cut-dirs=100 -e robots=off -l 0 -r -np -A 'node*linux-x64.tar.gz' https://nodejs.org/dist/latest/} if Dir.glob('*linux-x64.tar.gz').empty?
    nodejs = File.basename(Dir.glob('*linux-x64.tar.gz').last,'.tar.gz')
    sh %{tar -xzf #{Dir.glob('*linux-x64.tar.gz').last}} unless File.directory?(nodejs)
    FileUtils.ln_sf(nodejs,'latest')
  end

  Dir.chdir(BUILD_DIR) do
    ENV['PATH'] += %{:#{BASE_DIR}/node.js/latest/bin}

    sh %{npm install}
    # This is super hacky...
    %x{npm info --local grunt-cli} 
    sh %{npm install grunt-cli --save-dev} unless $?.success?

    ENV['PATH'] += %{:#{BUILD_DIR}/node_modules/.bin}
    sh %{grunt serve}
  end
end

task :default => 'build'

namespace :slide do
  slide_deck = {}
  sorted_slides(SLIDE_DIR) do |slide|
    slide_deck[slide.split('_').first.to_i] = slide
  end

  Dir.chdir(SLIDE_DIR) do

    desc <<-EOM
      Add a slide to the deck
      An optional ID may be provided for the slide and the other slides will be adjusted accordingly.
      EOM
    task :add,[:id] do
      puts 'TBD'
    end
  end
end
