# Review Live Reload
module RLR
  CSSFILE = 'main.css'

  def self.copy_css
    FileUtils.cp("src/#{CSSFILE}", "html/#{CSSFILE}")
  end

  def self.copy_images(name)
    self.mkdir_unless_exist('html/images')
    FileUtils.cp(name, 'html/images/')
  end

  def self.build_review(name)
    Dir.chdir('src') do
      `../bin/review-compile --target=html --stylesheet=#{CSSFILE} #{name}.re > ../html/#{name}.html`
      puts "built #{name}.html"
    end
  end

  def self.mkdir_unless_exist(path)
    FileUtils.mkdir_p(path) unless FileTest.exist?(path)
  end
end

guard 'shell' do
  # mkdir html
  RLR.mkdir_unless_exist('html')

  # HTML
  Dir.glob('src/*.re')    {|name| RLR.build_review name.gsub(/(^src\/|\.re$)/, '') }
  watch(/src\/(.+)\.re$/) {|name| RLR.build_review name[1] }

  # CSS
  RLR.copy_css
  watch("src/#{RLR::CSSFILE}") { RLR.copy_css }

  # Images
  Dir.glob('src/images/*') {|name| RLR.copy_images name }
  watch(/src\/images\/.*/) {|name| RLR.copy_images name }
end

guard 'livereload', :apply_js_live => false do
  watch(%r{html/.+})
end

