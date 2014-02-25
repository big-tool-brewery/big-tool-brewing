#OCLint needs to be built using CMake, and the version of LLVM it depends on also needs to to have been built using CMake

def test_cmake
  if `which cmake`.strip.empty?
    p 'You need to have cmake installed. Use `brew install cmake` to grab it.'
    abort
  end
end

desc 'Build and install LLVM'
task :llvm do
  test_cmake
  Dir.mkdir 'build' unless Dir.exists? 'build'
  Dir.chdir 'build' do |build_dir|
    Dir.mkdir 'llvm' unless Dir.exists? 'llvm'
    Dir.chdir 'llvm' do |llvm_dir|
      Dir.mkdir 'install_dir' unless Dir.exists? 'install_dir'
      sh ('cmake -DCMAKE_INSTALL_PREFIX:PATH=' + File.expand_path('./install_dir') + ' ' + File.expand_path('../../llvm'))
      sh 'make -j8 install'
    end
  end
end

desc 'Build and install OCLint'
task :oclint do
  Dir.chdir 'oclint/oclint-scripts' do |oclint_scripts_dir|
    sh('./makeWithExternClang ' + File.expand_path('../../build/llvm/install_dir'))
  end
end

task :distribution do
  require 'FileUtils'

  FileUtils.cp 'build/llvm/install_dir/bin/clang-format', 'distribution/'
end
