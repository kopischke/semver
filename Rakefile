# encoding: UTF-8
$:.push File.join(File.dirname(__FILE__), 'ext')

require 'bundler'
Bundler.setup(:development, :reporters)
require 'rake/clean'
require 'rake/testtask'
require 'yard/rake/yardoc_task'
require 'redcarpet'
require 'yard'

# Build system setup
VERBOSE = true

# Build system directory structure
BASE_DIR = File.join(File.expand_path(File.dirname(__FILE__)))
LIB_DIR  = File.join(BASE_DIR, 'lib')
DOCS_DIR = File.join(BASE_DIR, 'docs', 'yard')

# rake clobber
CLOBBER.include(File.join(DOCS_DIR, '**'))

# rake test
Rake::TestTask.new do |t|
  t.pattern = 'test/*_test.rb'
  t.verbose = VERBOSE
end

# rake yard
YARD::Rake::YardocTask.new do |t|
  # use relative path or YARD will display local system paths for source files
  t.files   =  [File.join(Pathname.new(LIB_DIR).relative_path_from(Pathname.new(BASE_DIR)), '**', '*.rb')]
  t.options.push('--output-dir', DOCS_DIR.shellescape)
  t.options.push('--markup', 'markdown', '--markup-provider', 'redcarpet')
  t.options.push('--verbose') if VERBOSE
end

# rake
task :default => [:test, :clobber, :yard]
