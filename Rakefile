require 'rubygems'
require 'rake/rdoctask'
require 'rake/gempackagetask'
require 'spec/rake/spectask'

PKG_NAME = 'merb_r18n'
gem 'r18n-core'
require 'r18n-core/version'

##############################################################################
# Tests
##############################################################################

desc 'Run all specs'
Spec::Rake::SpecTask.new('specs') do |t|
  t.spec_opts = ['--format', 'specdoc', '--colour']
  t.spec_files = Dir['spec/**/*_spec.rb'].sort
end

desc 'Run a specific spec with TASK=xxxx'
Spec::Rake::SpecTask.new('spec') do |t|
  t.spec_opts = ['--format', 'specdoc', '--colour']
  t.libs = ['lib']
  t.spec_files = ["spec/**/#{ENV['TASK']}_spec.rb"]
end

desc 'Run all specs output html'
Spec::Rake::SpecTask.new('specs_html') do |t|
  t.spec_opts = ['--format', 'html']
  t.libs = ['lib']
  t.spec_files = Dir['spec/**/*_spec.rb'].sort
end

desc 'RCov'
Spec::Rake::SpecTask.new('rcov') do |t|
  t.spec_opts = ['--format', 'specdoc', '--colour']
  t.spec_files = Dir['spec/**/*_spec.rb'].sort
  t.libs = ['lib']
  t.rcov = true
end

##############################################################################
# Documentation and distribution
##############################################################################

Rake::RDocTask.new do |rdoc|
  rdoc.main = 'README.rdoc'
  rdoc.rdoc_files.include('README.rdoc', 'LICENSE', 'lib/**/*.rb')
  rdoc.title = 'Merb R18n Plugin Documentation'
  rdoc.rdoc_dir = 'doc'
  rdoc.options << '-c utf-8'
  rdoc.options << '--all'
end

spec = Gem::Specification.new do |s|
  s.platform = Gem::Platform::RUBY
  s.name = PKG_NAME
  s.version = R18n::VERSION
  s.summary = 'A plugin for the Merb framework that provides i18n support to 
    translate your site.'
  s.description = <<-EOF
    A plugin for the Merb framework that provides i18n support to translate your
    site in several languages. It is just a wrap for R18n core library.
    It can format numbers and time to the rules of the user locale,
    has translation for common words, storage translation in YAML format with
    pluralization and procedures and has special support for countries
    with two official languages.
  EOF
  
  s.files = FileList[
    'lib/**/*',
    'LICENSE',
    'Rakefile',
    'README.rdoc']
  s.test_files = FileList[
    'spec/**/*']
  s.extra_rdoc_files = ['README.rdoc', 'LICENSE']
  s.require_path = 'lib'
  s.has_rdoc = true
  
  s.add_dependency 'merb-core'
  s.add_dependency 'r18n-core', R18n::VERSION
  
  s.author = 'Andrey "A.I." Sitnik'
  s.email = 'andrey@sitnik.ru'
  s.homepage = 'http://r18n.rubyforge.org/'
  s.rubyforge_project = 'r18n'
end

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.gem_spec = spec
end

desc 'Install merb_r18n as a gem'
task :install => [:package] do
  sudo = RUBY_PLATFORM =~ /win32/ ? '' : 'sudo'
  sh %{#{sudo} gem install pkg/#{PKG_NAME}-#{R18n::VERSION}}
end
