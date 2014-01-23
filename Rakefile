target :build do
  Dir.mkdir 'build' unless Dir.exists? 'build'
  Dir.chdir 'build' do |dir|
    sh '../llvm/configure'
    sh 'make -j8'
  end
end
