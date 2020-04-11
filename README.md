# Docker-stury-for-rails

## Ruby version
```bash
2.6.1
```

## Rails version
```bash
5.2.2
```

## Database creation
```bash
$ bundle exec rails db:create
```

## Database initialization
```bash
$ bundle exec rails db:migrate
```

## How to run the test suite
```bash
$ bundle exec rails test
```

## Execute rails server
```bash
$ bundle exec rails s
```

## エラー内容 2020年4月11日記載
### 現象
「Dockerfile」と「docker-compose.yml」を作成し、ビルド後、起動するとWEBサーバが起動しない。

### エラー内容
ビルド時(正常)
```
isseimiura@miuraichiseinoMacBook-Pro docker-study-for-rails % docker-compose build                                                                                                           
database uses an image, skipping
Building app
Step 1/11 : FROM  ruby:2.6.1-alpine
 ---> 152b059f918c
Step 2/11 : LABEL maintainer="Yuta_Ushijima<register@yuta-u.com>"
 ---> Using cache
 ---> d09be4fce533
Step 3/11 : ENV LANG="C.UTF-8"     LC_ALL=C.UTF-8     LC_CTYPE="utf-8"
 ---> Using cache
 ---> b6b04e2a41b0
Step 4/11 : ENV APP="/docker_example_for_rails"     CONTAINER_ROOT="./"     NOKOGIRI_OPTION="--use-system-libraries                     --with-xml2-config=/usr/bin/xml2-config                     --with-xslt-config=/usr/bin/xslt-config"     MYSQL_PORT="4306"     SERVER_PORT="4000"
 ---> Using cache
 ---> fa0658d0bc54
Step 5/11 : RUN apk update   && apk upgrade --no-cache   && apk add --update --no-cache       alpine-sdk       build-base       bash       imagemagick       jq       less       libgcrypt-dev       libxml2-dev             libxslt-dev       mariadb-dev       mysql-client       nodejs       redis       tzdata       wget             xvfb       yaml-dev             yarn             zlib-dev   && gem install -q -N bundler   && gem install -q -N pkg-config   && gem install -q -N rails -v 5.2.2.1   && gem install -q -N nokogiri -v 1.10.1 -- $NOKOGIRI_OPTION   && gem install -q -N mysql2 -v 0.4.10
 ---> Using cache
 ---> 9788ed715e27
Step 6/11 : WORKDIR $APP
 ---> Using cache
 ---> 26e34f9c3153
Step 7/11 : COPY Gemfile Gemfile.lock $CONTAINER_ROOT
 ---> Using cache
 ---> a4a0c70db930
Step 8/11 : RUN bundle install --jobs=4 --retry=3
 ---> Using cache
 ---> cf4e812fa9f3
Step 9/11 : ENV RAILS_SERVE_STATIC_FILES=true     PORT=$SERVER_PORT     TERM=xterm
 ---> Using cache
 ---> 48d0da4113fb
Step 10/11 : EXPOSE $SERVER_PORT
 ---> Using cache
 ---> 7e75cb4fb083
Step 11/11 : EXPOSE $MYSQL_PORT
 ---> Using cache
 ---> 1cb3a42a0352
Successfully built 1cb3a42a0352
Successfully tagged docker-study-for-rails_app:latest
```

起動時(異常)
```
isseimiura@miuraichiseinoMacBook-Pro docker-study-for-rails % docker-compose up   
Starting docker-study-for-rails_database_1 ... done
Starting docker-study-for-rails_app_1      ... done
Attaching to docker-study-for-rails_database_1, docker-study-for-rails_app_1
database_1  | 2020-04-11 12:10:24+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 5.7.29-1debian10 started.
database_1  | 2020-04-11 12:10:25+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
database_1  | 2020-04-11 12:10:25+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 5.7.29-1debian10 started.
database_1  | 2020-04-11T12:10:25.338713Z 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
database_1  | 2020-04-11T12:10:25.340745Z 0 [Note] mysqld (mysqld 5.7.29) starting as process 1 ...
database_1  | 2020-04-11T12:10:25.344513Z 0 [Note] InnoDB: PUNCH HOLE support available
database_1  | 2020-04-11T12:10:25.344556Z 0 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
database_1  | 2020-04-11T12:10:25.344564Z 0 [Note] InnoDB: Uses event mutexes
database_1  | 2020-04-11T12:10:25.344569Z 0 [Note] InnoDB: GCC builtin __atomic_thread_fence() is used for memory barrier
database_1  | 2020-04-11T12:10:25.344575Z 0 [Note] InnoDB: Compressed tables use zlib 1.2.11
database_1  | 2020-04-11T12:10:25.344584Z 0 [Note] InnoDB: Using Linux native AIO
database_1  | 2020-04-11T12:10:25.345292Z 0 [Note] InnoDB: Number of pools: 1
database_1  | 2020-04-11T12:10:25.345806Z 0 [Note] InnoDB: Using CPU crc32 instructions
database_1  | 2020-04-11T12:10:25.348408Z 0 [Note] InnoDB: Initializing buffer pool, total size = 128M, instances = 1, chunk size = 128M
database_1  | 2020-04-11T12:10:25.362055Z 0 [Note] InnoDB: Completed initialization of buffer pool
database_1  | 2020-04-11T12:10:25.364677Z 0 [Note] InnoDB: If the mysqld execution user is authorized, page cleaner thread priority can be changed. See the man page of setpriority().
database_1  | 2020-04-11T12:10:25.376708Z 0 [Note] InnoDB: Highest supported file format is Barracuda.
database_1  | 2020-04-11T12:10:25.386103Z 0 [Note] InnoDB: Creating shared tablespace for temporary tables
database_1  | 2020-04-11T12:10:25.386180Z 0 [Note] InnoDB: Setting file './ibtmp1' size to 12 MB. Physically writing the file full; Please wait ...
database_1  | 2020-04-11T12:10:25.406892Z 0 [Note] InnoDB: File './ibtmp1' size is now 12 MB.
database_1  | 2020-04-11T12:10:25.407896Z 0 [Note] InnoDB: 96 redo rollback segment(s) found. 96 redo rollback segment(s) are active.
database_1  | 2020-04-11T12:10:25.407936Z 0 [Note] InnoDB: 32 non-redo rollback segment(s) are active.
database_1  | 2020-04-11T12:10:25.408423Z 0 [Note] InnoDB: Waiting for purge to start
database_1  | 2020-04-11T12:10:25.458825Z 0 [Note] InnoDB: 5.7.29 started; log sequence number 12481163
database_1  | 2020-04-11T12:10:25.459309Z 0 [Note] Plugin 'FEDERATED' is disabled.
database_1  | 2020-04-11T12:10:25.459552Z 0 [Note] InnoDB: Loading buffer pool(s) from /var/lib/mysql/ib_buffer_pool
database_1  | 2020-04-11T12:10:25.465826Z 0 [Note] InnoDB: Buffer pool(s) load completed at 200411 12:10:25
database_1  | 2020-04-11T12:10:25.466754Z 0 [Note] Found ca.pem, server-cert.pem and server-key.pem in data directory. Trying to enable SSL support using them.
database_1  | 2020-04-11T12:10:25.466793Z 0 [Note] Skipping generation of SSL certificates as certificate files are present in data directory.
database_1  | 2020-04-11T12:10:25.467741Z 0 [Warning] CA certificate ca.pem is self signed.
database_1  | 2020-04-11T12:10:25.467798Z 0 [Note] Skipping generation of RSA key pair as key files are present in data directory.
database_1  | 2020-04-11T12:10:25.468285Z 0 [Note] Server hostname (bind-address): '*'; port: 3306
database_1  | 2020-04-11T12:10:25.468371Z 0 [Note] IPv6 is available.
database_1  | 2020-04-11T12:10:25.468461Z 0 [Note]   - '::' resolves to '::';
database_1  | 2020-04-11T12:10:25.468487Z 0 [Note] Server socket created on IP: '::'.
database_1  | 2020-04-11T12:10:25.470287Z 0 [Warning] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
database_1  | 2020-04-11T12:10:25.487062Z 0 [Note] Event Scheduler: Loaded 0 events
database_1  | 2020-04-11T12:10:25.487323Z 0 [Note] mysqld: ready for connections.
database_1  | Version: '5.7.29'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
app_1       | yarn install v1.12.3
app_1       | [1/4] Resolving packages...
app_1       | success Already up-to-date.
app_1       | Done in 0.08s.
app_1       | Usage:
app_1       |   rails new APP_PATH [options]
app_1       | 
app_1       | Options:
app_1       |       [--skip-namespace], [--no-skip-namespace]            # Skip namespace (affects only isolated applications)
app_1       |   -r, [--ruby=PATH]                                        # Path to the Ruby binary of your choice
app_1       |                                                            # Default: /usr/local/bin/ruby
app_1       |   -m, [--template=TEMPLATE]                                # Path to some application template (can be a filesystem path or URL)
app_1       |   -d, [--database=DATABASE]                                # Preconfigure for selected database (options: mysql/postgresql/sqlite3/oracle/frontbase/ibm_db/sqlserver/jdbcmysql/jdbcsqlite3/jdbcpostgresql/jdbc)
app_1       |                                                            # Default: sqlite3
app_1       |       [--skip-yarn], [--no-skip-yarn]                      # Don't use Yarn for managing JavaScript dependencies
app_1       |       [--skip-gemfile], [--no-skip-gemfile]                # Don't create a Gemfile
app_1       |   -G, [--skip-git], [--no-skip-git]                        # Skip .gitignore file
app_1       |       [--skip-keeps], [--no-skip-keeps]                    # Skip source control .keep files
app_1       |   -M, [--skip-action-mailer], [--no-skip-action-mailer]    # Skip Action Mailer files
app_1       |   -O, [--skip-active-record], [--no-skip-active-record]    # Skip Active Record files
app_1       |       [--skip-active-storage], [--no-skip-active-storage]  # Skip Active Storage files
app_1       |   -P, [--skip-puma], [--no-skip-puma]                      # Skip Puma related files
app_1       |   -C, [--skip-action-cable], [--no-skip-action-cable]      # Skip Action Cable files
app_1       |   -S, [--skip-sprockets], [--no-skip-sprockets]            # Skip Sprockets files
app_1       |       [--skip-spring], [--no-skip-spring]                  # Don't install Spring application preloader
app_1       |       [--skip-listen], [--no-skip-listen]                  # Don't generate configuration that depends on the listen gem
app_1       |       [--skip-coffee], [--no-skip-coffee]                  # Don't use CoffeeScript
app_1       |   -J, [--skip-javascript], [--no-skip-javascript]          # Skip JavaScript files
app_1       |       [--skip-turbolinks], [--no-skip-turbolinks]          # Skip turbolinks gem
app_1       |   -T, [--skip-test], [--no-skip-test]                      # Skip test files
app_1       |       [--skip-system-test], [--no-skip-system-test]        # Skip system test files
app_1       |       [--skip-bootsnap], [--no-skip-bootsnap]              # Skip bootsnap gem
app_1       |       [--dev], [--no-dev]                                  # Setup the application with Gemfile pointing to your Rails checkout
app_1       |       [--edge], [--no-edge]                                # Setup the application with Gemfile pointing to Rails repository
app_1       |       [--rc=RC]                                            # Path to file containing extra configuration options for rails command
app_1       |       [--no-rc], [--no-no-rc]                              # Skip loading of extra configuration options from .railsrc file
app_1       |       [--api], [--no-api]                                  # Preconfigure smaller stack for API only apps
app_1       |   -B, [--skip-bundle], [--no-skip-bundle]                  # Don't run bundle install
app_1       |       [--webpack=WEBPACK]                                  # Preconfigure for app-like JavaScript with Webpack (options: react/vue/angular/elm/stimulus)
app_1       | 
app_1       | Runtime options:
app_1       |   -f, [--force]                    # Overwrite files that already exist
app_1       |   -p, [--pretend], [--no-pretend]  # Run but do not make any changes
app_1       |   -q, [--quiet], [--no-quiet]      # Suppress status output
app_1       |   -s, [--skip], [--no-skip]        # Skip files that already exist
app_1       | 
app_1       | Rails options:
app_1       |   -h, [--help], [--no-help]        # Show this help message and quit
app_1       |   -v, [--version], [--no-version]  # Show Rails version number and quit
app_1       | 
app_1       | Description:
app_1       |     The 'rails new' command creates a new Rails application with a default
app_1       |     directory structure and configuration at the path you specify.
app_1       | 
app_1       |     You can specify extra command-line arguments to be used every time
app_1       |     'rails new' runs in the .railsrc configuration file in your home directory.
app_1       | 
app_1       |     Note that the arguments specified in the .railsrc file don't affect the
app_1       |     defaults values shown above in this help message.
app_1       | 
app_1       | Example:
app_1       |     rails new ~/Code/Ruby/weblog
app_1       | 
app_1       |     This generates a skeletal Rails installation in ~/Code/Ruby/weblog.
app_1       | Usage:
app_1       |   rails new APP_PATH [options]
app_1       | 
app_1       | Options:
app_1       |       [--skip-namespace], [--no-skip-namespace]            # Skip namespace (affects only isolated applications)
app_1       |   -r, [--ruby=PATH]                                        # Path to the Ruby binary of your choice
app_1       |                                                            # Default: /usr/local/bin/ruby
app_1       |   -m, [--template=TEMPLATE]                                # Path to some application template (can be a filesystem path or URL)
app_1       |   -d, [--database=DATABASE]                                # Preconfigure for selected database (options: mysql/postgresql/sqlite3/oracle/frontbase/ibm_db/sqlserver/jdbcmysql/jdbcsqlite3/jdbcpostgresql/jdbc)
app_1       |                                                            # Default: sqlite3
app_1       |       [--skip-yarn], [--no-skip-yarn]                      # Don't use Yarn for managing JavaScript dependencies
app_1       |       [--skip-gemfile], [--no-skip-gemfile]                # Don't create a Gemfile
app_1       |   -G, [--skip-git], [--no-skip-git]                        # Skip .gitignore file
app_1       |       [--skip-keeps], [--no-skip-keeps]                    # Skip source control .keep files
app_1       |   -M, [--skip-action-mailer], [--no-skip-action-mailer]    # Skip Action Mailer files
app_1       |   -O, [--skip-active-record], [--no-skip-active-record]    # Skip Active Record files
app_1       |       [--skip-active-storage], [--no-skip-active-storage]  # Skip Active Storage files
app_1       |   -P, [--skip-puma], [--no-skip-puma]                      # Skip Puma related files
app_1       |   -C, [--skip-action-cable], [--no-skip-action-cable]      # Skip Action Cable files
app_1       |   -S, [--skip-sprockets], [--no-skip-sprockets]            # Skip Sprockets files
app_1       |       [--skip-spring], [--no-skip-spring]                  # Don't install Spring application preloader
app_1       |       [--skip-listen], [--no-skip-listen]                  # Don't generate configuration that depends on the listen gem
app_1       |       [--skip-coffee], [--no-skip-coffee]                  # Don't use CoffeeScript
app_1       |   -J, [--skip-javascript], [--no-skip-javascript]          # Skip JavaScript files
app_1       |       [--skip-turbolinks], [--no-skip-turbolinks]          # Skip turbolinks gem
app_1       |   -T, [--skip-test], [--no-skip-test]                      # Skip test files
app_1       |       [--skip-system-test], [--no-skip-system-test]        # Skip system test files
app_1       |       [--skip-bootsnap], [--no-skip-bootsnap]              # Skip bootsnap gem
app_1       |       [--dev], [--no-dev]                                  # Setup the application with Gemfile pointing to your Rails checkout
app_1       |       [--edge], [--no-edge]                                # Setup the application with Gemfile pointing to Rails repository
app_1       |       [--rc=RC]                                            # Path to file containing extra configuration options for rails command
app_1       |       [--no-rc], [--no-no-rc]                              # Skip loading of extra configuration options from .railsrc file
app_1       |       [--api], [--no-api]                                  # Preconfigure smaller stack for API only apps
app_1       |   -B, [--skip-bundle], [--no-skip-bundle]                  # Don't run bundle install
app_1       |       [--webpack=WEBPACK]                                  # Preconfigure for app-like JavaScript with Webpack (options: react/vue/angular/elm/stimulus)
app_1       | 
app_1       | Runtime options:
app_1       |   -f, [--force]                    # Overwrite files that already exist
app_1       |   -p, [--pretend], [--no-pretend]  # Run but do not make any changes
app_1       |   -q, [--quiet], [--no-quiet]      # Suppress status output
app_1       |   -s, [--skip], [--no-skip]        # Skip files that already exist
app_1       | 
app_1       | Rails options:
app_1       |   -h, [--help], [--no-help]        # Show this help message and quit
app_1       |   -v, [--version], [--no-version]  # Show Rails version number and quit
app_1       | 
app_1       | Description:
app_1       |     The 'rails new' command creates a new Rails application with a default
app_1       |     directory structure and configuration at the path you specify.
app_1       | 
app_1       |     You can specify extra command-line arguments to be used every time
app_1       |     'rails new' runs in the .railsrc configuration file in your home directory.
app_1       | 
app_1       |     Note that the arguments specified in the .railsrc file don't affect the
app_1       |     defaults values shown above in this help message.
app_1       | 
app_1       | Example:
app_1       |     rails new ~/Code/Ruby/weblog
app_1       | 
app_1       |     This generates a skeletal Rails installation in ~/Code/Ruby/weblog.
docker-study-for-rails_app_1 exited with code 0
```