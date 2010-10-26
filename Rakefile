%w[rubygems rake rake/clean fileutils newgem rubigen hoe].each { |f| require f }
require File.dirname(__FILE__) + '/lib/freshbooks'

# Generate all the Rake tasks
# Run 'rake -T' to see list of generated tasks (from gem root directory)
$hoe = Hoe.new('freshbooks.rb', FreshBooks::VERSION) do |p|
  p.developer('Ben Curren', 'ben@outright.com')
  p.changes              = p.paragraphs_of("History.txt", 0..1).join("\n\n")
  p.rubyforge_name       = p.name # TODO this is default value
  p.extra_deps         = ['activesupport']
  p.extra_dev_deps = [
    ['newgem', ">= #{::Newgem::VERSION}"],
    ['mocha', ">= 0.9.4"]
  ]
  
  p.clean_globs |= %w[**/.DS_Store tmp *.log]
  path = (p.rubyforge_name == p.name) ? p.rubyforge_name : "\#{p.rubyforge_name}/\#{p.name}"
  p.remote_rdoc_dir = File.join(path.gsub(/^#{p.rubyforge_name}\/?/,''), 'rdoc')
  p.rsync_args = '-av --delete --ignore-errors'
end

require 'newgem/tasks' # load /tasks/*.rake
Dir['tasks/**/*.rake'].each { |t| load t }

# TODO - want other tests/tasks run by default? Add them to the list
# task :default => [:spec, :features]
