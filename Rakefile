require 'rake'
require 'rake/packagetask'
require 'rake/clean'

HOME_DIR = File.expand_path(File.dirname(__FILE__))
BUILD_DIR = File.join(HOME_DIR, 'build')
SRC_DIR = File.join(HOME_DIR, 'src')
LIB_DIR = File.join(HOME_DIR, 'lib')
BIN_DIR = File.join(HOME_DIR, 'bin')
CLOSURE_LIBRARY_DIR = File.join(HOME_DIR, '..', 'closure-library-read-only/closure')

CLEAN.include(BUILD_DIR)

task :default => :compile

desc 'Compile using closure compiler'
task :compile do
  verbose(false) { mkdir_p(BUILD_DIR) }
  closure_compiler = File.join(BIN_DIR, 'closure-compiler', 'compiler.jar')

  files = [
    "--js #{File.join(SRC_DIR, 'history.js')}"
  ]

  compiler_flags = [
    "--compilation_level=ADVANCED_OPTIMIZATIONS",
    "--warning_level=VERBOSE",
    "--summary_detail_level=3",
    "--js_output_file=#{File.join(BUILD_DIR, 'history-min.js')}",
    "--define='DEBUG=false'",
    "--externs=#{File.join(SRC_DIR, 'externs.js')}"
  ]

  sh "java -jar #{closure_compiler} #{files.join(' ')} #{compiler_flags.join(' ')}"

  # Make gzip version
  sh "cat #{File.join(BUILD_DIR, 'history-min.js')} | gzip -f > #{File.join(BUILD_DIR, 'history-min.js.gz')}"
end
