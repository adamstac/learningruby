require 'stringex'

task :default => ["new:memoir"]

namespace :new do

  desc "Create a new memoir"
  task :memoir do
    puts "Enter the memoir name:"
    title = STDIN.gets

    filename = "memoirs/#{title.to_url}.md"

    if File.exist?(filename)
      abort("Opps, that memoir already exists.")
    end

    puts "Creating the new memoir: #{filename}"

    open(filename, 'w') do |memoir|
      memoir.puts "# #{title}\n"
    end
  end

end
