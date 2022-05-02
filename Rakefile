require 'active_record'
require 'yaml'
require 'pry-byebug'

databases = ActiveRecord::Tasks::DatabaseTasks.setup_initial_database_yaml

namespace :db do

    desc "Create the db"
    task :create do
        puts "just creating ..."
        connection_details = YAML::load(File.open('config/database.yml'))
        admin_connection = connection_details.merge({'database'=> 'postgres','schema_search_path'=> 'public'})
        puts admin_connection
        ActiveRecord::Base.establish_connection(admin_connection)
        ActiveRecord::Base.connection.create_database(connection_details.fetch('database'))
    end

    desc "Migrating the db"
    task :migrate do
        puts "just migrating ..."
        connection_details = YAML::load(File.open('config/database.yml'))
        print_establish_connections=ActiveRecord::Base.establish_connection(connection_details)
        puts print_establish_connections
        p=ActiveRecord::MigrationContext.new("db/migrate/").migrate(001)
        puts p
    end

    desc 'Display status of migration'
    task :status  do
        # puts "status ..."
        # for x in ActiveRecord::Base.connection.tables
        #     puts x
        # end
        
    end
    
end