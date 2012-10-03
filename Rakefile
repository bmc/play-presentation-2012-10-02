# -*- ruby -*-

task :default => :build

PANDOC_OPTS = [
  '-i',
  '--self-contained',
  '-t', 'slidy',
  '--smart'
]

task :build => :css do
  require 'tempfile'

  tmp = Tempfile.new('slides')
  tmp.close
  begin
    args = PANDOC_OPTS + ['-s', 'slides.md', '-o', tmp.path]
    sh 'pandoc', *args
    puts "Inserting custom stylesheet and generating slides.html"
    File.open("slides.html", "w") do |out|
      File.open(tmp.path).each do |line|
        if line =~ %r{^</head>}
          custom_css = File.open('custom.css').read
          out.write <<-EOF
<style type="text/css">
#{custom_css}
</style>
          EOF
        end
        out.write(line)
      end
    end
  ensure
    tmp.unlink
  end
end

task :css => ['custom.css']

file 'custom.css' => ['custom.less'] do
  sh 'sh', '-c', 'lessc custom.less >custom.css'
end
