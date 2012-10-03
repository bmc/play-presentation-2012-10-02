# -*- ruby -*-

task :default => :run

task :build do
  sh 'sh', '-c', 'lessc custom.less> custom.css'
end

task :run => :build do
  sh 'showoff', 'serve'
end

task :static => :build do
  sh 'showoff', 'static'
end

