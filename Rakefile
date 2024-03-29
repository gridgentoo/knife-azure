#
# Copyright:: Copyright 2010-2019, Chef Software Inc.
# License:: Apache License, Version 2.0
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

require "bundler/gem_tasks"
require "rspec/core/rake_task"

begin
  Bundler.setup(:default, :development)
rescue Bundler::BundlerError => e
  warn e.message
  warn "Run `bundle install` to install missing gems"
  exit e.status_code
end

Bundler::GemHelper.install_tasks

desc "Run specs"
RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = FileList["spec/unit/**/*_spec.rb"].to_a
end

RSpec::Core::RakeTask.new(:functional) do |spec|
  spec.pattern = FileList["spec/functional/**/*_test.rb"].to_a
end

RSpec::Core::RakeTask.new(:integration) do |spec|
  spec.pattern = FileList["spec/integration/**/*_test.rb"].to_a
end

RSpec::Core::RakeTask.new(:rcov) do |spec|
  spec.pattern = "spec/unit|functional/*_spec.rb"
  spec.rcov = true
end

begin
  require "chefstyle"
  require "rubocop/rake_task"
  RuboCop::RakeTask.new(:style) do |task|
    task.options += ["--display-cop-names", "--no-color"]
  end
rescue LoadError
  puts "chefstyle/rubocop is not available. bundle install first to make sure all dependencies are installed."
end

begin
  require "yard"
  YARD::Rake::YardocTask.new(:docs)
rescue LoadError
  puts "yard is not available. bundle install first to make sure all dependencies are installed."
end

task :console do
  require "irb"
  require "irb/completion"
  ARGV.clear
  IRB.start
end

task default: %i{style spec}
