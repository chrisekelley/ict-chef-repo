


require "bundler/setup"

task :default => [:list]


desc "Lists all the tasks."
task :list do
  puts "Tasks: \n- #{(Rake::Task.tasks).join("\n- ")}"
end

desc "Checks for required dependencies."
task :check do
  environemnt_vars = [
    'KNIFE_CLIENT_KEY',
    'KNIFE_VALIDATION_KEY',
    'KNIFE_CHEF_SERVER',
    'KNIFE_COOKBOOK_COPYRIGHT',
    'KNIFE_COOKBOOK_LICENSE',
    'KNIFE_COOKBOOK_EMAIL',
    'KNIFE_CACHE_PATH'
  ]
  errors = []
  environemnt_vars.each do |var|
    if ENV[var].nil?
      errors.push(" - \e\[31m#Variable: {var} not set!\e\[0m\n")
    else
      puts " - \e\[32mVariable: #{var} set to \"#{ENV[var]}\"\e\[0m\n"
    end
  end

  # client_key "#{ENV['HOME']}/.chef/#{user}.pem"
  # validation_client_name "#{ENV['ORGNAME']}-validator"
  # validation_key "#{ENV['HOME']}/.chef/#{ENV['ORGNAME']}-validator.pem"
  # chef_server_url "https://api.opscode.com/organizations/#{ENV['ORGNAME']}"


  file_list = [
    "#{ENV['KNIFE_CLIENT_KEY']}",
    "#{ENV['KNIFE_VALIDATION_KEY']}",
  ]

    file_list.each do |file|
      if File.exist?(file)
        puts " - \e\[32mFile: \"#{file}\" found.\e\[0m\n"
      else
        errors.push(" - \e\[31mRequired file: \"#{file}\" not found!\e\[0m\n")
      end
    end

    if system("command -v virtualbox >/dev/null 2>&1")
      puts " - \e\[32mProgram: \"virtualbox\" found.\e\[0m\n"
    else
      errors.push(" - \e\[31mProgram: \"virtualbox\" not found!\e\[0m\n")
    end

    if system("command -v vagrant >/dev/null 2>&1")
      puts " - \e\[32mProgram: \"vagrant\" found.\e\[0m\n"
      %x{vagrant --version}.match(/\d+\.\d+\.\d+/) { |m|
        if Gem::Version.new(m.to_s) < Gem::Version.new('1.1.0')
          errors.push(" -- \e\[31mVagrant version \"#{m.to_s}\" is too old!\e\[0m\n")
        else
          puts " - \e\[32mVagrant \"#{m.to_s}\" works!\e\[0m\n"
        end
      }
    else
      errors.push(" - \e\[31mProgram: \"vagrant\" not found!\e\[0m\n")
    end

  unless errors.empty?
    puts "The following errors occured:\n#{errors.join()}"
  end
end

desc "Builds the package."
task :build do
  Rake::Task[:knife_test].execute
  Rake::Task[:chefspec].execute
  Rake::Task[:foodcritic].execute
end

desc "Fires up the Vagrant box."
task :start do
  sh "vagrant up"
end

desc "Runs knife cookbook test against all the cookbooks."
task :knife_test do
  sh "bundle exec knife cookbook test -a"
end

desc "Runs chefspec on all the cookbooks."
task :chefspec do
  sh "bundle exec rspec cookbooks"
end

desc "Runs foodcritic against all the cookbooks."
task :foodcritic do
  sh "bundle exec foodcritic cookbooks"
end


