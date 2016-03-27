require 'fileutils'

ROOT_DIR = File.expand_path('..', __FILE__)
SRC_DIR  = "#{ROOT_DIR}/src"
DIST_DIR = "#{ROOT_DIR}/dist"
RES_DIR  = "#{ROOT_DIR}/resources"

FileUtils.mkdir_p(DIST_DIR)

def compile(file)
  name = File.basename(file, '.md')
  dist = "#{DIST_DIR}/#{name}"
  FileUtils.mkdir_p(dist)

  `pandoc -s "#{file}" -o "#{dist}/output.html"`
  `pandoc -s "#{file}" -o "#{dist}/output.tex"`
  `xelatex -synctex=1 --interaction=nonstopmode -output-directory="#{dist}" "#{dist}/output.tex"`
end

desc "generate html/tex/pdf from the markdown source"
task :gen do
  Dir["#{SRC_DIR}/*.md"].each do |file|
    compile(file)
  end
end
