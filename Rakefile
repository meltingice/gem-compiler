require "rubygems/package_task"

gemspec = Gem::Specification.load("gem-compiler.gemspec")

Gem::PackageTask.new(gemspec) do |pkg|
end

desc "Environment information"
task :info do
  puts "Ruby: #{RUBY_VERSION}"
  puts "RubyGems: #{Gem::VERSION}"
  puts "$LOAD_PATH: #{$LOAD_PATH.join(File::PATH_SEPARATOR)}"
  puts "---" * 10
  puts "PATH: #{ENV['PATH']}"
  puts "RUBYOPT: #{ENV['RUBYOPT']}"
  puts "RUBYLIB: #{ENV['RUBYLIB']}"
  puts "GEM_HOME: #{ENV['GEM_HOME']}"
  puts "GEM_PATH: #{ENV['GEM_PATH']}"

  # List any Bundle specific information
  ENV.select { |k, _| k =~ /BUNDLE/ }.each do |key, value|
    puts "#{key}: #{value}"
  end

  puts "---" * 10
end

desc "Run tests"
task :test => [:info] do
  lib_dirs = ["lib", "test"].join(File::PATH_SEPARATOR)
  test_files = FileList["test/**/test*.rb"].gsub("test/", "")

  ruby "-I#{lib_dirs} -e \"ARGV.each { |f| require f }\" #{test_files}"
end

task :default => [:test]
