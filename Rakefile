require 'rake'
require 'rspec/core/rake_task'
require 'yaml'

properties = YAML.load_file('properties.yml')

desc "Run serverspec on all hosts"
task :serverspec    => 'serverspec:all'
task :default => :serverspec

namespace :serverspec do
  task :all => properties.keys.map {|key| 'serverspec:' + key.split('.')[0] }
  properties.keys.each do |key|
    desc "Run serverspec to #{key}"
    RSpec::Core::RakeTask.new(key.split('.')[0].to_sym) do |t|
      ENV['TARGET_HOST'] = key
      puts ""
      puts "Running tests on:"
      puts "    " + key
      puts ""
      t.pattern = 'spec/{' + properties[key][:roles].join(',') + '}/*_spec.rb'
    end
  end
end
