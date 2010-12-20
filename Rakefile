require 'rubygems'
require 'bundler'
Bundler.setup

require 'environment'

desc 'Start a development server'
task :server do
	if which('shotgun')
		exec 'shotgun -s thin -O config.ru'
	else
		warn 'warn: shotgun not installed; reloading is disabled.'
		exec 'rackup config.ru -s thin -p 9393'
	end
end

desc 'Index documentation'
task :index do
  puts "indexing now:"
  client = IndexTank::Client.new(ENV['HEROKUTANK_API_URL'])
  index = client.indexes(AppConfig['index'])
  index.add unless index.exists?
  Topic.all_topics.each do |doc|
    if File.exist?(doc)
      name = name_for(doc)
      puts "...indexing #{name}"
      source = File.read(doc)
      topic = Topic.load(name, source)
      topic.text_only
      result = indextank_document = index.document(name).add(:title => topic.title, :text => topic.body)
      puts "=> #{result}"
    end
  end
  puts "finished indexing"
end

desc 'Sample search'
task :search, :query do |t, args|
  client = IndexTank::Client.new(ENV['HEROKUTANK_API_URL'])
  index = client.indexes(AppConfig['index'])
  results = index.search(args[:query], :fetch => 'title', :snippet => 'text')
  puts "#{results['matches']} results."
  puts results.inspect
end

desc 'Alias for server'
task :start => :server

def which(command)
	ENV['PATH'].
		split(':').
		map  { |p| "#{p}/#{command}" }.
		find { |p| File.executable?(p) }
end

def name_for(doc)
  File.basename(doc, '.txt')
end

